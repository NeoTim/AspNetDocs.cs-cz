---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-1
title: 'Část 1: Přehled a vytvoření projektu | Dokumentace Microsoftu'
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/03/2012
ms.assetid: 94421d86-68c4-4471-bf5f-82d654a17252
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-1
msc.type: authoredcontent
ms.openlocfilehash: 0e4021402e8deccd2395f23b6b512679b5e9d281
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57073807"
---
<a name="part-1-overview-and-creating-the-project"></a><span data-ttu-id="edd94-102">Část 1: Přehled a vytvoření projektu</span><span class="sxs-lookup"><span data-stu-id="edd94-102">Part 1: Overview and Creating the Project</span></span>
====================
<span data-ttu-id="edd94-103">podle [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="edd94-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="edd94-104">Stáhnout dokončený projekt</span><span class="sxs-lookup"><span data-stu-id="edd94-104">Download Completed Project</span></span>](http://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

<span data-ttu-id="edd94-105">Entity Framework je objektově/relační mapování rozhraní.</span><span class="sxs-lookup"><span data-stu-id="edd94-105">Entity Framework is an object/relational mapping framework.</span></span> <span data-ttu-id="edd94-106">Mapuje se na entity v relační databázi objektů domény ve vašem kódu.</span><span class="sxs-lookup"><span data-stu-id="edd94-106">It maps the domain objects in your code to entities in a relational database.</span></span> <span data-ttu-id="edd94-107">Ve většině případů není nutné se starat o databázové vrstvě, protože rozhraní Entity Framework za vás postará o ho.</span><span class="sxs-lookup"><span data-stu-id="edd94-107">For the most part, you do not have to worry about the database layer, because Entity Framework takes care of it for you.</span></span> <span data-ttu-id="edd94-108">Váš kód provádí úpravy objektů a změny se ukládají do databáze.</span><span class="sxs-lookup"><span data-stu-id="edd94-108">Your code manipulates the objects, and changes are persisted to a database.</span></span>

## <a name="about-the-tutorial"></a><span data-ttu-id="edd94-109">Informace o kurzu</span><span class="sxs-lookup"><span data-stu-id="edd94-109">About the Tutorial</span></span>

<span data-ttu-id="edd94-110">V tomto kurzu vytvoříte jednoduchou úložiště aplikací.</span><span class="sxs-lookup"><span data-stu-id="edd94-110">In this tutorial, you will create a simple store application.</span></span> <span data-ttu-id="edd94-111">Existují dvě hlavní části aplikace.</span><span class="sxs-lookup"><span data-stu-id="edd94-111">There are two main parts to the application.</span></span> <span data-ttu-id="edd94-112">Normální uživatelé mohou zobrazit produkty a vytvoření objednávky:</span><span class="sxs-lookup"><span data-stu-id="edd94-112">Normal users can view products and create orders:</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image1.png)

<span data-ttu-id="edd94-113">Správci mohou vytvořit, odstranit nebo upravit produkty:</span><span class="sxs-lookup"><span data-stu-id="edd94-113">Administrators can create, delete, or edit products:</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image2.png)

## <a name="skills-youll-learn"></a><span data-ttu-id="edd94-114">Dovednosti, které se dozvíte</span><span class="sxs-lookup"><span data-stu-id="edd94-114">Skills You'll Learn</span></span>

<span data-ttu-id="edd94-115">Zde je, co se dozvíte:</span><span class="sxs-lookup"><span data-stu-id="edd94-115">Here's what you'll learn:</span></span>

- <span data-ttu-id="edd94-116">Jak používat rozhraní Entity Framework s webovým rozhraním API technologie ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="edd94-116">How to use Entity Framework with ASP.NET Web API.</span></span>
- <span data-ttu-id="edd94-117">Jak používat rozhraní knockout.js k vytvoření dynamického uživatelského rozhraní klienta.</span><span class="sxs-lookup"><span data-stu-id="edd94-117">How to use knockout.js to create a dynamic client UI.</span></span>
- <span data-ttu-id="edd94-118">Jak používat ověřování pomocí formulářů s webovým rozhraním API pro ověřování uživatelů.</span><span class="sxs-lookup"><span data-stu-id="edd94-118">How to use forms authentication with Web API to authenticate users.</span></span>

<span data-ttu-id="edd94-119">I když v tomto kurzu je samostatný, můžete chtít nejdřív přečíst následující kurzy:</span><span class="sxs-lookup"><span data-stu-id="edd94-119">Although this tutorial is self-contained, you might want to read the following tutorials first:</span></span>

- [<span data-ttu-id="edd94-120">Vaše první rozhraní ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="edd94-120">Your First ASP.NET Web API</span></span>](../../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)
- [<span data-ttu-id="edd94-121">Vytvoření webového rozhraní API, která podporuje operace CRUD</span><span class="sxs-lookup"><span data-stu-id="edd94-121">Creating a Web API that Supports CRUD Operations</span></span>](../creating-a-web-api-that-supports-crud-operations.md)

<span data-ttu-id="edd94-122">Základní znalost [ASP.NET MVC](../../../../mvc/index.md) je také užitečné.</span><span class="sxs-lookup"><span data-stu-id="edd94-122">Some knowledge of [ASP.NET MVC](../../../../mvc/index.md) is also helpful.</span></span>

## <a name="overview"></a><span data-ttu-id="edd94-123">Přehled</span><span class="sxs-lookup"><span data-stu-id="edd94-123">Overview</span></span>

<span data-ttu-id="edd94-124">Na vysoké úrovni je tady Architektura aplikace:</span><span class="sxs-lookup"><span data-stu-id="edd94-124">At a high level, here is the architecture of the application:</span></span>

- <span data-ttu-id="edd94-125">ASP.NET MVC vygeneruje stránky HTML klienta.</span><span class="sxs-lookup"><span data-stu-id="edd94-125">ASP.NET MVC generates the HTML pages for the client.</span></span>
- <span data-ttu-id="edd94-126">Rozhraní ASP.NET Web API zveřejňuje operace CRUD s daty (výrobky a objednávky).</span><span class="sxs-lookup"><span data-stu-id="edd94-126">ASP.NET Web API exposes CRUD operations on the data (products and orders).</span></span>
- <span data-ttu-id="edd94-127">Entity Framework překládá modely C# používá webového rozhraní API do entity databáze.</span><span class="sxs-lookup"><span data-stu-id="edd94-127">Entity Framework translates the C# models used by Web API into database entities.</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image3.png)

<span data-ttu-id="edd94-128">Následující diagram znázorňuje, jak jsou reprezentovány objekty domény v různých vrstvách aplikace: Databázové vrstvě, objektový model a nakonec přenosový formát, který se používá k přenosu dat do klienta prostřednictvím protokolu HTTP.</span><span class="sxs-lookup"><span data-stu-id="edd94-128">The following diagram shows how the domain objects are represented at various layers of the application: The database layer, the object model, and finally the wire format, which is used to transmit data to the client via HTTP.</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image4.png)

## <a name="create-the-visual-studio-project"></a><span data-ttu-id="edd94-129">Vytvoření projektu sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="edd94-129">Create the Visual Studio Project</span></span>

<span data-ttu-id="edd94-130">Můžete vytvořit projekt kurz pomocí Visual Web Developer Express nebo plná verze Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="edd94-130">You can create the tutorial project using either Visual Web Developer Express or the full version of Visual Studio.</span></span>

<span data-ttu-id="edd94-131">Z **Start** klikněte na **nový projekt**.</span><span class="sxs-lookup"><span data-stu-id="edd94-131">From the **Start** page, click **New Project**.</span></span>

<span data-ttu-id="edd94-132">V **šablony** vyberte **nainstalované šablony** a rozbalte **Visual C#** uzlu.</span><span class="sxs-lookup"><span data-stu-id="edd94-132">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="edd94-133">V části **Visual C#** vyberte **webové**.</span><span class="sxs-lookup"><span data-stu-id="edd94-133">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="edd94-134">V seznamu šablon projektu vyberte **webové aplikace ASP.NET MVC 4**.</span><span class="sxs-lookup"><span data-stu-id="edd94-134">In the list of project templates, select **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="edd94-135">Pojmenujte projekt "ProductStore" a klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="edd94-135">Name the project "ProductStore" and click **OK**.</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image5.png)

<span data-ttu-id="edd94-136">V **nového projektu ASP.NET MVC 4** dialogového okna, vyberte **internetovou aplikaci** a klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="edd94-136">In the **New ASP.NET MVC 4 Project** dialog, select **Internet Application** and click **OK**.</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image6.png)

<span data-ttu-id="edd94-137">"Internetové aplikace" šablona vytvoří aplikaci ASP.NET MVC, která podporuje ověřování pomocí formulářů.</span><span class="sxs-lookup"><span data-stu-id="edd94-137">The "Internet Application" template creates an ASP.NET MVC application that supports forms authentication.</span></span> <span data-ttu-id="edd94-138">Pokud nyní aplikaci spustíte, už má některé funkce:</span><span class="sxs-lookup"><span data-stu-id="edd94-138">If you run the application now, it already has some features:</span></span>

- <span data-ttu-id="edd94-139">Noví uživatelé můžete zaregistrovat klepnutím na odkaz "Register" v pravém horním rohu.</span><span class="sxs-lookup"><span data-stu-id="edd94-139">New users can register by clicking the "Register" link in the upper right corner.</span></span>
- <span data-ttu-id="edd94-140">Registrovaní uživatelé přihlásit po klepnutí na odkaz "Přihlásit".</span><span class="sxs-lookup"><span data-stu-id="edd94-140">Registered users can log in by clicking the "Log in" link.</span></span>

<span data-ttu-id="edd94-141">Informace o členství se ukládají v databázi, která se vytvoří automaticky.</span><span class="sxs-lookup"><span data-stu-id="edd94-141">Membership information is persisted in a database that gets created automatically.</span></span> <span data-ttu-id="edd94-142">Další informace o ověřování pomocí formulářů v ASP.NET MVC naleznete v tématu [názorný postup: Použití ověřování pomocí formulářů v ASP.NET MVC](https://msdn.microsoft.com/library/ff398049(VS.98).aspx).</span><span class="sxs-lookup"><span data-stu-id="edd94-142">For more information about forms authentication in ASP.NET MVC, see [Walkthrough: Using Forms Authentication in ASP.NET MVC](https://msdn.microsoft.com/library/ff398049(VS.98).aspx).</span></span>

## <a name="update-the-css-file"></a><span data-ttu-id="edd94-143">Aktualizovat soubor CSS</span><span class="sxs-lookup"><span data-stu-id="edd94-143">Update the CSS File</span></span>

<span data-ttu-id="edd94-144">Tento krok je kosmetické, ale budou stránky se pak takto předchozí snímky obrazovky.</span><span class="sxs-lookup"><span data-stu-id="edd94-144">This step is cosmetic, but it will make the pages render like the earlier screen shots.</span></span>

<span data-ttu-id="edd94-145">V Průzkumníku řešení rozbalte složku obsahu a otevřete soubor s názvem Site.css.</span><span class="sxs-lookup"><span data-stu-id="edd94-145">In Solution Explorer, expand the Content folder and open the file named Site.css.</span></span> <span data-ttu-id="edd94-146">Přidejte následující stylů CSS:</span><span class="sxs-lookup"><span data-stu-id="edd94-146">Add the following CSS styles:</span></span>

[!code-css[Main](using-web-api-with-entity-framework-part-1/samples/sample1.css)]

> [!div class="step-by-step"]
> [<span data-ttu-id="edd94-147">Next</span><span class="sxs-lookup"><span data-stu-id="edd94-147">Next</span></span>](using-web-api-with-entity-framework-part-2.md)
