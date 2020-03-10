---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/creating-an-odata-endpoint
title: Vytvoření koncového bodu OData V3 s webovým rozhraním API 2 | Microsoft Docs
author: MikeWasson
description: Protokol OData (Open Data Protocol) je protokol pro přístup k datům pro web. OData poskytuje jednotný způsob strukturování dat, dotazování na data a manipulaci s daty...
ms.author: riande
ms.date: 02/25/2014
ms.assetid: 262843d6-43a2-4f1c-82d9-0b90ae6df0cf
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/creating-an-odata-endpoint
msc.type: authoredcontent
ms.openlocfilehash: e68a454398f109dfd089be9c9a44d3fe662acc2f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556411"
---
# <a name="creating-an-odata-v3-endpoint-with-web-api-2"></a><span data-ttu-id="7b4d0-104">Vytvoření koncového bodu OData V3 pomocí webového rozhraní API 2</span><span class="sxs-lookup"><span data-stu-id="7b4d0-104">Creating an OData v3 Endpoint with Web API 2</span></span>

<span data-ttu-id="7b4d0-105">o [Jan Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="7b4d0-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="7b4d0-106">Stáhnout dokončený projekt</span><span class="sxs-lookup"><span data-stu-id="7b4d0-106">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> <span data-ttu-id="7b4d0-107">Protokol OData ( [Open Data Protocol](http://www.odata.org/) ) je protokol pro přístup k datům pro web.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-107">The [Open Data Protocol](http://www.odata.org/) (OData) is a data access protocol for the web.</span></span> <span data-ttu-id="7b4d0-108">OData poskytuje jednotný způsob strukturování dat, dotazování na data a manipulaci s datovou sadou prostřednictvím operací CRUD (vytvoření, čtení, aktualizace a odstranění).</span><span class="sxs-lookup"><span data-stu-id="7b4d0-108">OData provides a uniform way to structure data, query the data, and manipulate the data set through CRUD operations (create, read, update, and delete).</span></span> <span data-ttu-id="7b4d0-109">OData podporuje formáty AtomPub (XML) i JSON.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-109">OData supports both AtomPub (XML) and JSON formats.</span></span> <span data-ttu-id="7b4d0-110">OData také definuje způsob, jak vystavit metadata o datech.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-110">OData also defines a way to expose metadata about the data.</span></span> <span data-ttu-id="7b4d0-111">Klienti můžou metadata použít ke zjištění informací o typu a vztahů pro datovou sadu.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-111">Clients can use the metadata to discover the type information and relationships for the data set.</span></span>
>
> <span data-ttu-id="7b4d0-112">Webové rozhraní API pro ASP.NET usnadňuje vytvoření koncového bodu OData pro datovou sadu.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-112">ASP.NET Web API makes it easy to create an OData endpoint for a data set.</span></span> <span data-ttu-id="7b4d0-113">Můžete přesně řídit, které operace OData koncový bod podporuje.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-113">You can control exactly which OData operations the endpoint supports.</span></span> <span data-ttu-id="7b4d0-114">Můžete hostovat více koncových bodů OData spolu s koncovými body mimo OData.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-114">You can host multiple OData endpoints, alongside non-OData endpoints.</span></span> <span data-ttu-id="7b4d0-115">Máte plnou kontrolu nad datovým modelem, koncovou obchodní logikou a datovou vrstvou.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-115">You have full control over your data model, back-end business logic, and data layer.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="7b4d0-116">Verze softwaru použité v tomto kurzu</span><span class="sxs-lookup"><span data-stu-id="7b4d0-116">Software versions used in the tutorial</span></span>
>
>
> - [<span data-ttu-id="7b4d0-117">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="7b4d0-117">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="7b4d0-118">Webové rozhraní API 2</span><span class="sxs-lookup"><span data-stu-id="7b4d0-118">Web API 2</span></span>
> - <span data-ttu-id="7b4d0-119">OData verze 3</span><span class="sxs-lookup"><span data-stu-id="7b4d0-119">OData Version 3</span></span>
> - <span data-ttu-id="7b4d0-120">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="7b4d0-120">Entity Framework 6</span></span>
> - [<span data-ttu-id="7b4d0-121">Proxy Fiddler webového ladění (volitelné)</span><span class="sxs-lookup"><span data-stu-id="7b4d0-121">Fiddler Web Debugging Proxy (Optional)</span></span>](http://www.fiddler2.com)
>
> <span data-ttu-id="7b4d0-122">V [aktualizaci ASP.NET and Web Tools 2012,2](https://go.microsoft.com/fwlink/?LinkId=282650)byla přidána podpora rozhraní Web API OData.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-122">Web API OData support was added in [ASP.NET and Web Tools 2012.2 Update](https://go.microsoft.com/fwlink/?LinkId=282650).</span></span> <span data-ttu-id="7b4d0-123">Tento kurz ale používá generování uživatelského rozhraní, které bylo přidáno v Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-123">However, this tutorial uses scaffolding that was added in Visual Studio 2013.</span></span>

<span data-ttu-id="7b4d0-124">V tomto kurzu vytvoříte jednoduchý koncový bod OData, ke kterému se můžou klienti dotazovat.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-124">In this tutorial, you will create a simple OData endpoint that clients can query.</span></span> <span data-ttu-id="7b4d0-125">Také vytvoříte C# klienta pro koncový bod.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-125">You will also create a C# client for the endpoint.</span></span> <span data-ttu-id="7b4d0-126">Po dokončení tohoto kurzu se v další sadě kurzů ukáže, jak přidat další funkce, včetně vztahů mezi entitami, akcemi a $expand/$select.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-126">After you complete this tutorial, the next set of tutorials show how to add more functionality, including entity relations, actions, and $expand/$select.</span></span>

- [<span data-ttu-id="7b4d0-127">Vytvoření projektu sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7b4d0-127">Create the Visual Studio Project</span></span>](#create-project)
- [<span data-ttu-id="7b4d0-128">Přidání modelu entity</span><span class="sxs-lookup"><span data-stu-id="7b4d0-128">Add an Entity Model</span></span>](#add-model)
- [<span data-ttu-id="7b4d0-129">Přidat kontroler OData</span><span class="sxs-lookup"><span data-stu-id="7b4d0-129">Add an OData Controller</span></span>](#add-controller)
- [<span data-ttu-id="7b4d0-130">Přidání modelu EDM a trasy</span><span class="sxs-lookup"><span data-stu-id="7b4d0-130">Add the EDM and Route</span></span>](#edm)
- [<span data-ttu-id="7b4d0-131">Dosazení databáze (volitelné)</span><span class="sxs-lookup"><span data-stu-id="7b4d0-131">Seed the Database (Optional)</span></span>](#seed-db)
- [<span data-ttu-id="7b4d0-132">Zkoumání koncového bodu OData</span><span class="sxs-lookup"><span data-stu-id="7b4d0-132">Exploring the OData Endpoint</span></span>](#explore)
- [<span data-ttu-id="7b4d0-133">Formáty serializace OData</span><span class="sxs-lookup"><span data-stu-id="7b4d0-133">OData Serialization Formats</span></span>](#formats)

<a id="create-project"></a>
## <a name="create-the-visual-studio-project"></a><span data-ttu-id="7b4d0-134">Vytvoření projektu sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7b4d0-134">Create the Visual Studio Project</span></span>

<span data-ttu-id="7b4d0-135">V tomto kurzu vytvoříte koncový bod OData, který podporuje základní operace CRUD.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-135">In this tutorial, you will create an OData endpoint that supports basic CRUD operations.</span></span> <span data-ttu-id="7b4d0-136">Koncový bod zveřejní jeden prostředek, seznam produktů.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-136">The endpoint will expose a single resource, a list of products.</span></span> <span data-ttu-id="7b4d0-137">Novější kurzy budou přidávat další funkce.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-137">Later tutorials will add more features.</span></span>

<span data-ttu-id="7b4d0-138">Spusťte Visual Studio a na úvodní stránce vyberte **Nový projekt** .</span><span class="sxs-lookup"><span data-stu-id="7b4d0-138">Start Visual Studio and select **New Project** from the Start page.</span></span> <span data-ttu-id="7b4d0-139">Nebo v nabídce **soubor** vyberte **Nový** a pak **projekt**.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-139">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="7b4d0-140">V podokně **šablony** vyberte **Nainstalované šablony** a rozbalte uzel vizuál C# .</span><span class="sxs-lookup"><span data-stu-id="7b4d0-140">In the **Templates** pane, select **Installed Templates** and expand the Visual C# node.</span></span> <span data-ttu-id="7b4d0-141">V **části C#vizuál** vyberte **Web**.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-141">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="7b4d0-142">Vyberte šablonu **webové aplikace ASP.NET** .</span><span class="sxs-lookup"><span data-stu-id="7b4d0-142">Select **the ASP.NET Web Application** template.</span></span>

![](creating-an-odata-endpoint/_static/image1.png)

<span data-ttu-id="7b4d0-143">V dialogovém okně **Nový projekt ASP.NET** vyberte **prázdnou** šablonu.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-143">In the **New ASP.NET Project** dialog, select the **Empty** template.</span></span> <span data-ttu-id="7b4d0-144">V části &quot;přidat složky a základní reference pro...&quot;zaškrtněte **webové rozhraní API**.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-144">Under &quot;Add folders and core references for...&quot;, check **Web API**.</span></span> <span data-ttu-id="7b4d0-145">Klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-145">Click **OK**.</span></span>

![](creating-an-odata-endpoint/_static/image2.png)

<a id="add-model"></a>
## <a name="add-an-entity-model"></a><span data-ttu-id="7b4d0-146">Přidání modelu entity</span><span class="sxs-lookup"><span data-stu-id="7b4d0-146">Add an Entity Model</span></span>

<span data-ttu-id="7b4d0-147">*Model* je objekt, který představuje data v aplikaci.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-147">A *model* is an object that represents the data in your application.</span></span> <span data-ttu-id="7b4d0-148">Pro tento kurz potřebujeme model, který reprezentuje produkt.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-148">For this tutorial, we need a model that represents a product.</span></span> <span data-ttu-id="7b4d0-149">Model odpovídá našemu typu entity OData.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-149">The model corresponds to our OData entity type.</span></span>

<span data-ttu-id="7b4d0-150">V Průzkumník řešení klikněte pravým tlačítkem na složku modely.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-150">In Solution Explorer, right-click the Models folder.</span></span> <span data-ttu-id="7b4d0-151">V místní nabídce vyberte **Přidat** a pak vyberte **Třída**.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-151">From the context menu, select **Add** then select **Class**.</span></span>

![](creating-an-odata-endpoint/_static/image3.png)

<span data-ttu-id="7b4d0-152">V dialogovém okně **Přidat novou** položku pojmenujte třídu &quot;&quot;produktu.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-152">In the **Add New** Item dialog, name the class &quot;Product&quot;.</span></span>

![](creating-an-odata-endpoint/_static/image4.png)

> [!NOTE]
> <span data-ttu-id="7b4d0-153">Podle konvence jsou třídy modelu umístěny do složky modely.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-153">By convention, model classes are placed in the Models folder.</span></span> <span data-ttu-id="7b4d0-154">Nemusíte postupovat podle této konvence ve svých vlastních projektech, ale použijeme ji pro tento kurz.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-154">You don't have to follow this convention in your own projects, but we'll use it for this tutorial.</span></span>

<span data-ttu-id="7b4d0-155">Do souboru Product.cs přidejte následující definici třídy:</span><span class="sxs-lookup"><span data-stu-id="7b4d0-155">In the Product.cs file, add the following class definition:</span></span>

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample1.cs)]

<span data-ttu-id="7b4d0-156">Vlastnost ID bude klíč entity.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-156">The ID property will be the entity key.</span></span> <span data-ttu-id="7b4d0-157">Klienti můžou zadávat dotazy na produkty podle ID.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-157">Clients can query products by ID.</span></span> <span data-ttu-id="7b4d0-158">Toto pole by také představovalo primární klíč v back-endové databázi.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-158">This field would also be the primary key in the back-end database.</span></span>

<span data-ttu-id="7b4d0-159">Sestavte projekt hned teď.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-159">Build the project now.</span></span> <span data-ttu-id="7b4d0-160">V dalším kroku použijeme některé generování uživatelského rozhraní sady Visual Studio, které používá reflexi k nalezení typu produktu.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-160">In the next step, we'll use some Visual Studio scaffolding that uses reflection to find the Product type.</span></span>

<a id="add-controller"></a>
## <a name="add-an-odata-controller"></a><span data-ttu-id="7b4d0-161">Přidat kontroler OData</span><span class="sxs-lookup"><span data-stu-id="7b4d0-161">Add an OData Controller</span></span>

<span data-ttu-id="7b4d0-162">*Kontroler* je třída, která zpracovává požadavky HTTP.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-162">A *controller* is a class that handles HTTP requests.</span></span> <span data-ttu-id="7b4d0-163">Pro každou sadu entit v rámci služby OData definujete samostatný kontroler.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-163">You define a separate controller for each entity set in you OData service.</span></span> <span data-ttu-id="7b4d0-164">V tomto kurzu vytvoříme jeden kontroler.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-164">In this tutorial, we'll create a single controller.</span></span>

<span data-ttu-id="7b4d0-165">V Průzkumník řešení klikněte pravým tlačítkem myši na složku Controllers.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-165">In Solution Explorer, right-click the Controllers folder.</span></span> <span data-ttu-id="7b4d0-166">Vyberte **Přidat** a pak vybrat **kontroler**.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-166">Select **Add** and then select **Controller**.</span></span>

![](creating-an-odata-endpoint/_static/image5.png)

<span data-ttu-id="7b4d0-167">V dialogovém okně **Přidat generování uživatelského rozhraní** vyberte &quot;kontroler webového rozhraní API 2 OData s akcemi pomocí Entity Framework&quot;.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-167">In the **Add Scaffold** dialog, select &quot;Web API 2 OData Controller with actions, using Entity Framework&quot;.</span></span>

![](creating-an-odata-endpoint/_static/image6.png)

<span data-ttu-id="7b4d0-168">V dialogovém okně **Přidat řadič** pojmenujte kontroler "ProductsController".</span><span class="sxs-lookup"><span data-stu-id="7b4d0-168">In the **Add Controller** dialog, name the controller "ProductsController".</span></span> <span data-ttu-id="7b4d0-169">Vyberte &quot;použít akce asynchronního kontroleru&quot; CheckBox.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-169">Select the &quot;Use async controller actions&quot; checkbox.</span></span> <span data-ttu-id="7b4d0-170">V rozevíracím seznamu **model** vyberte třídu produktu.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-170">In the **Model** drop-down list, select the Product class.</span></span>

![](creating-an-odata-endpoint/_static/image7.png)

<span data-ttu-id="7b4d0-171">Klikněte na tlačítko **nový kontext dat...** .</span><span class="sxs-lookup"><span data-stu-id="7b4d0-171">Click the **New data context...** button.</span></span> <span data-ttu-id="7b4d0-172">Ponechte výchozí název typu datového kontextu a klikněte na **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-172">Leave the default name for the data context type, and click **Add**.</span></span>

![](creating-an-odata-endpoint/_static/image8.png)

<span data-ttu-id="7b4d0-173">Kliknutím na Přidat v dialogovém okně Přidat řadič přidejte kontroler.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-173">Click Add in the Add Controller dialog to add the controller.</span></span>

![](creating-an-odata-endpoint/_static/image9.png)

<span data-ttu-id="7b4d0-174">Poznámka: Pokud se zobrazí chybová zpráva s oznámením &quot;došlo k chybě při získávání typu...&quot;, ujistěte se, že jste po přidání třídy produktu vytvořili projekt sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-174">Note: If you get an error message that says &quot;There was an error getting the type...&quot;, make sure that you built the Visual Studio project after you added the Product class.</span></span> <span data-ttu-id="7b4d0-175">Generování uživatelského rozhraní používá reflexi k nalezení třídy.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-175">The scaffolding uses reflection to find the class.</span></span>

![](creating-an-odata-endpoint/_static/image10.png)

<span data-ttu-id="7b4d0-176">Generování uživatelského rozhraní do projektu přidá dva soubory kódu:</span><span class="sxs-lookup"><span data-stu-id="7b4d0-176">The scaffolding adds two code files to the project:</span></span>

- <span data-ttu-id="7b4d0-177">Products.cs definuje kontroler webového rozhraní API, který implementuje koncový bod OData.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-177">Products.cs defines the Web API controller that implements the OData endpoint.</span></span>
- <span data-ttu-id="7b4d0-178">ProductServiceContext.cs poskytuje metody pro dotazování podkladové databáze pomocí Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-178">ProductServiceContext.cs provides methods to query the underlying database, using Entity Framework.</span></span>

![](creating-an-odata-endpoint/_static/image11.png)

<a id="edm"></a>
## <a name="add-the-edm-and-route"></a><span data-ttu-id="7b4d0-179">Přidání modelu EDM a trasy</span><span class="sxs-lookup"><span data-stu-id="7b4d0-179">Add the EDM and Route</span></span>

<span data-ttu-id="7b4d0-180">V Průzkumník řešení rozbalte složku App\_Start Folder a otevřete soubor s názvem WebApiConfig.cs.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-180">In Solution Explorer, expand the App\_Start folder and open the file named WebApiConfig.cs.</span></span> <span data-ttu-id="7b4d0-181">Tato třída obsahuje konfigurační kód pro webové rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-181">This class holds configuration code for Web API.</span></span> <span data-ttu-id="7b4d0-182">Nahraďte tento kód následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="7b4d0-182">Replace this code with the following:</span></span>

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample2.cs)]

<span data-ttu-id="7b4d0-183">Tento kód provede dvě věci:</span><span class="sxs-lookup"><span data-stu-id="7b4d0-183">This code does two things:</span></span>

- <span data-ttu-id="7b4d0-184">Vytvoří model EDM (Entity Data Model) (EDM) pro koncový bod OData.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-184">Creates an Entity Data Model (EDM) for the OData endpoint.</span></span>
- <span data-ttu-id="7b4d0-185">Přidá trasu pro koncový bod.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-185">Adds a route for the endpoint.</span></span>

<span data-ttu-id="7b4d0-186">EDM je abstraktní model dat.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-186">An EDM is an abstract model of the data.</span></span> <span data-ttu-id="7b4d0-187">Model EDM slouží k vytvoření dokumentu metadat a definování identifikátorů URI pro službu.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-187">The EDM is used to create the metadata document and define the URIs for the service.</span></span> <span data-ttu-id="7b4d0-188">**ODataConventionModelBuilder** vytvoří EDM pomocí sady výchozích konvencí pojmenování EDM.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-188">The **ODataConventionModelBuilder** creates an EDM by using a set of default naming conventions EDM.</span></span> <span data-ttu-id="7b4d0-189">Tento přístup vyžaduje nejméně kód.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-189">This approach requires the least code.</span></span> <span data-ttu-id="7b4d0-190">Pokud chcete mít větší kontrolu nad modelem EDM, můžete pomocí třídy **ODataModelBuilder** vytvořit EDM přidáním vlastností, klíčů a vlastností navigace explicitně.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-190">If you want more control over the EDM, you can use the **ODataModelBuilder** class to create the EDM by adding properties, keys, and navigation properties explicitly.</span></span>

<span data-ttu-id="7b4d0-191">Metoda **EntitySet** přidá sadu entit do modelu EDM:</span><span class="sxs-lookup"><span data-stu-id="7b4d0-191">The **EntitySet** method adds an entity set to the EDM:</span></span>

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample3.cs)]

<span data-ttu-id="7b4d0-192">Řetězec "Products" definuje název sady entit.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-192">The string "Products" defines the name of the entity set.</span></span> <span data-ttu-id="7b4d0-193">Název kontroleru se musí shodovat s názvem sady entit.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-193">The name of the controller must match the name of the entity set.</span></span> <span data-ttu-id="7b4d0-194">V tomto kurzu se sada entit nazývá "Products" a kontroler má název `ProductsController`.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-194">In this tutorial, the entity set is named "Products" and the controller is named `ProductsController`.</span></span> <span data-ttu-id="7b4d0-195">Pokud jste pojmenovali sadu entit "ProductSet", pojmenujete `ProductSetController`kontroleru.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-195">If you named the entity set "ProductSet", you would name the controller `ProductSetController`.</span></span> <span data-ttu-id="7b4d0-196">Všimněte si, že koncový bod může mít několik sad entit.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-196">Note that an endpoint can have multiple entity sets.</span></span> <span data-ttu-id="7b4d0-197">Pro každou sadu entit volejte **&gt;EntitySet&lt;t** a pak definujte odpovídající kontroler.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-197">Call **EntitySet&lt;T&gt;** for each entity set, and then define a corresponding controller.</span></span>

<span data-ttu-id="7b4d0-198">Metoda **MapODataRoute** přidá trasu pro koncový bod OData.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-198">The **MapODataRoute** method adds a route for the OData endpoint.</span></span>

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample4.cs)]

<span data-ttu-id="7b4d0-199">První parametr je popisný název trasy.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-199">The first parameter is a friendly name for the route.</span></span> <span data-ttu-id="7b4d0-200">Klienti vaší služby tento název nevidí.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-200">Clients of your service do not see this name.</span></span> <span data-ttu-id="7b4d0-201">Druhým parametrem je předpona identifikátoru URI pro koncový bod.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-201">The second parameter is the URI prefix for the endpoint.</span></span> <span data-ttu-id="7b4d0-202">V tomto kódu je identifikátor URI pro sadu entit Products http://<em>hostname</em>/OData/Products.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-202">Given this code, the URI for the Products entity set is http://<em>hostname</em>/odata/Products.</span></span> <span data-ttu-id="7b4d0-203">Vaše aplikace může mít více než jeden koncový bod OData.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-203">Your application can have more than one OData endpoint.</span></span> <span data-ttu-id="7b4d0-204">Pro každý koncový bod zavolejte <strong>MapODataRoute</strong> a zadejte jedinečný název trasy a jedinečnou PŘEDPONu identifikátoru URI.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-204">For each endpoint, call <strong>MapODataRoute</strong> and provide a unique route name and a unique URI prefix.</span></span>

<a id="seed-db"></a>
## <a name="seed-the-database-optional"></a><span data-ttu-id="7b4d0-205">Dosazení databáze (volitelné)</span><span class="sxs-lookup"><span data-stu-id="7b4d0-205">Seed the Database (Optional)</span></span>

<span data-ttu-id="7b4d0-206">V tomto kroku použijete Entity Framework k osazení databáze s některými testovacími daty.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-206">In this step, you will use Entity Framework to seed the database with some test data.</span></span> <span data-ttu-id="7b4d0-207">Tento krok je nepovinný, ale umožňuje hned testovat koncový bod OData.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-207">This step is optional, but it lets you test out your OData endpoint right away.</span></span>

<span data-ttu-id="7b4d0-208">V nabídce **nástroje** vyberte **Správce balíčků NuGet**a pak vyberte **Konzola správce balíčků**.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-208">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="7b4d0-209">V okně konzoly Správce balíčků zadejte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="7b4d0-209">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample5.cmd)]

<span data-ttu-id="7b4d0-210">Tím se přidá složka s názvem migrace a soubor kódu s názvem Configuration.cs.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-210">This adds a folder named Migrations and a code file named Configuration.cs.</span></span>

![](creating-an-odata-endpoint/_static/image12.png)

<span data-ttu-id="7b4d0-211">Otevřete tento soubor a přidejte následující kód do metody `Configuration.Seed`.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-211">Open this file and add the following code to the `Configuration.Seed` method.</span></span>

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample6.cs)]

<span data-ttu-id="7b4d0-212">V okně konzoly Správce balíčků zadejte následující příkazy:</span><span class="sxs-lookup"><span data-stu-id="7b4d0-212">In the Package Manager Console Window, enter the following commands:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample7.cmd)]

<span data-ttu-id="7b4d0-213">Tyto příkazy generují kód, který vytvoří databázi a následně spustí tento kód.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-213">These commands generate code that creates the database, and then executes that code.</span></span>

<a id="explore"></a>
## <a name="exploring-the-odata-endpoint"></a><span data-ttu-id="7b4d0-214">Zkoumání koncového bodu OData</span><span class="sxs-lookup"><span data-stu-id="7b4d0-214">Exploring the OData Endpoint</span></span>

<span data-ttu-id="7b4d0-215">V této části použijeme [proxy Fiddler webového ladění](http://www.fiddler2.com) k odeslání požadavků do koncového bodu a kontrole zpráv odpovědí.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-215">In this section, we'll use the [Fiddler Web Debugging Proxy](http://www.fiddler2.com) to send requests to the endpoint and examine the response messages.</span></span> <span data-ttu-id="7b4d0-216">To vám pomůže pochopit možnosti koncového bodu OData.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-216">This will help you to understand the capabilities of an OData endpoint.</span></span>

<span data-ttu-id="7b4d0-217">V aplikaci Visual Studio stiskněte klávesu F5 pro spuštění ladění.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-217">In Visual Studio, press F5 to start debugging.</span></span> <span data-ttu-id="7b4d0-218">Ve výchozím nastavení Visual Studio otevře váš prohlížeč na `http://localhost:*port*`, kde *port* je číslo portu nakonfigurované v nastavení projektu.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-218">By default, Visual Studio opens your browser to `http://localhost:*port*`, where *port* is the port number configured in the project settings.</span></span>

<span data-ttu-id="7b4d0-219">V nastavení projektu můžete změnit číslo portu.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-219">You can change the port number in the project settings.</span></span> <span data-ttu-id="7b4d0-220">V Průzkumník řešení klikněte pravým tlačítkem myši na projekt a vyberte **vlastnosti**.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-220">In Solution Explorer, right-click the project and select **Properties**.</span></span> <span data-ttu-id="7b4d0-221">V okně Vlastnosti vyberte **Web**.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-221">In the properties window, select **Web**.</span></span> <span data-ttu-id="7b4d0-222">Do pole **Adresa URL projektu**zadejte číslo portu.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-222">Enter the port number under **Project Url**.</span></span>

### <a name="service-document"></a><span data-ttu-id="7b4d0-223">Dokument služby</span><span class="sxs-lookup"><span data-stu-id="7b4d0-223">Service Document</span></span>

<span data-ttu-id="7b4d0-224">*Dokument služby* obsahuje seznam sad entit pro koncový bod OData.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-224">The *service document* contains a list of the entity sets for the OData endpoint.</span></span> <span data-ttu-id="7b4d0-225">Chcete-li získat dokument služby, odešlete požadavek GET do kořenového identifikátoru URI služby.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-225">To get the service document, send a GET request to the root URI of the service.</span></span>

<span data-ttu-id="7b4d0-226">Pomocí Fiddler na kartě **skladatele** zadejte následující identifikátor URI: `http://localhost:port/odata/`, kde *port* je číslo portu.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-226">Using Fiddler, enter the following URI in the **Composer** tab: `http://localhost:port/odata/`, where *port* is the port number.</span></span>

![](creating-an-odata-endpoint/_static/image13.png)

<span data-ttu-id="7b4d0-227">Klikněte na tlačítko **Provést**.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-227">Click the **Execute** button.</span></span> <span data-ttu-id="7b4d0-228">Fiddler odešle do vaší aplikace požadavek HTTP GET.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-228">Fiddler sends an HTTP GET request to your application.</span></span> <span data-ttu-id="7b4d0-229">V seznamu webové relace by se měla zobrazit odpověď.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-229">You should see the response in the Web Sessions list.</span></span> <span data-ttu-id="7b4d0-230">Pokud vše funguje, bude stavový kód 200.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-230">If everything is working, the status code will be 200.</span></span>

![](creating-an-odata-endpoint/_static/image14.png)

<span data-ttu-id="7b4d0-231">Dvojitým kliknutím na odpověď v seznamu webové relace zobrazíte podrobnosti zprávy s odpovědí na kartě kontroly.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-231">Double-click the response in the Web Sessions list to see the details of the response message in the Inspectors tab.</span></span>

![](creating-an-odata-endpoint/_static/image15.png)

<span data-ttu-id="7b4d0-232">Zpráva s nezpracovanými odpověďmi HTTP by měla vypadat nějak takto:</span><span class="sxs-lookup"><span data-stu-id="7b4d0-232">The raw HTTP response message should look similar to the following:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample8.cmd)]

<span data-ttu-id="7b4d0-233">Ve výchozím nastavení webový rozhraní API vrátí dokument služby ve formátu AtomPub.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-233">By default, Web API returns the service document in AtomPub format.</span></span> <span data-ttu-id="7b4d0-234">Pro vyžádání JSON přidejte do požadavku HTTP následující hlavičku:</span><span class="sxs-lookup"><span data-stu-id="7b4d0-234">To request JSON, add the following header to the HTTP request:</span></span>

`Accept: application/json`

![](creating-an-odata-endpoint/_static/image16.png)

<span data-ttu-id="7b4d0-235">Nyní odpověď HTTP obsahuje datovou část JSON:</span><span class="sxs-lookup"><span data-stu-id="7b4d0-235">Now the HTTP response contains a JSON payload:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample9.cmd)]

### <a name="service-metadata-document"></a><span data-ttu-id="7b4d0-236">Dokument metadat služby</span><span class="sxs-lookup"><span data-stu-id="7b4d0-236">Service Metadata Document</span></span>

<span data-ttu-id="7b4d0-237">*Dokument metadat služby* popisuje datový model služby pomocí jazyka XML nazývaného jazyk CSDL (konceptuální schéma Definition Language).</span><span class="sxs-lookup"><span data-stu-id="7b4d0-237">The *service metadata document* describes the data model of the service, using an XML language called the Conceptual Schema Definition Language (CSDL).</span></span> <span data-ttu-id="7b4d0-238">Dokument metadat zobrazuje strukturu dat ve službě a lze jej použít k vygenerování kódu klienta.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-238">The metadata document shows the structure of the data in the service, and can be used to generate client code.</span></span>

<span data-ttu-id="7b4d0-239">Chcete-li získat dokument metadat, odešlete požadavek GET na `http://localhost:port/odata/$metadata`.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-239">To get the metadata document, send a GET request to `http://localhost:port/odata/$metadata`.</span></span> <span data-ttu-id="7b4d0-240">Tady je metadata pro koncový bod zobrazený v tomto kurzu.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-240">Here is the metadata for the endpoint shown in this tutorial.</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample10.cmd)]

### <a name="entity-set"></a><span data-ttu-id="7b4d0-241">Sada entit</span><span class="sxs-lookup"><span data-stu-id="7b4d0-241">Entity Set</span></span>

<span data-ttu-id="7b4d0-242">Chcete-li získat sadu entit Products, odešlete požadavek GET na `http://localhost:port/odata/Products`.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-242">To get the Products entity set, send a GET request to `http://localhost:port/odata/Products`.</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample11.cmd)]

### <a name="entity"></a><span data-ttu-id="7b4d0-243">Entita</span><span class="sxs-lookup"><span data-stu-id="7b4d0-243">Entity</span></span>

<span data-ttu-id="7b4d0-244">Pokud chcete získat jednotlivý produkt, pošlete požadavek GET na `http://localhost:port/odata/Products(1)`, kde "1" je ID produktu.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-244">To get an individual product, send a GET request to `http://localhost:port/odata/Products(1)`, where "1" is the product ID.</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample12.cmd)]

<a id="formats"></a>
## <a name="odata-serialization-formats"></a><span data-ttu-id="7b4d0-245">Formáty serializace OData</span><span class="sxs-lookup"><span data-stu-id="7b4d0-245">OData Serialization Formats</span></span>

<span data-ttu-id="7b4d0-246">OData podporuje několik formátů serializace:</span><span class="sxs-lookup"><span data-stu-id="7b4d0-246">OData supports several serialization formats:</span></span>

- <span data-ttu-id="7b4d0-247">Publikování atomů (XML)</span><span class="sxs-lookup"><span data-stu-id="7b4d0-247">Atom Pub (XML)</span></span>
- <span data-ttu-id="7b4d0-248">JSON "Light" (představený v OData V3)</span><span class="sxs-lookup"><span data-stu-id="7b4d0-248">JSON "light" (introduced in OData v3)</span></span>
- <span data-ttu-id="7b4d0-249">JSON "Verbose" (OData v2)</span><span class="sxs-lookup"><span data-stu-id="7b4d0-249">JSON "verbose" (OData v2)</span></span>

<span data-ttu-id="7b4d0-250">Ve výchozím nastavení používá webové rozhraní API AtomPubJSON formát "Light".</span><span class="sxs-lookup"><span data-stu-id="7b4d0-250">By default, Web API uses AtomPubJSON "light" format.</span></span>

<span data-ttu-id="7b4d0-251">Chcete-li získat formát AtomPub, nastavte hlavičku Accept na "Application/Atom + XML".</span><span class="sxs-lookup"><span data-stu-id="7b4d0-251">To get AtomPub format, set the Accept header to "application/atom+xml".</span></span> <span data-ttu-id="7b4d0-252">Tady je příklad těla odpovědi:</span><span class="sxs-lookup"><span data-stu-id="7b4d0-252">Here is an example response body:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample13.cmd)]

<span data-ttu-id="7b4d0-253">Můžete se podívat na jednu zjevnou nevýhodu formátu Atom: je to mnohem více podrobných podrobností než ve formátu JSON.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-253">You can see one obvious disadvantage of the Atom format: It's a lot more verbose than the JSON light.</span></span> <span data-ttu-id="7b4d0-254">Pokud však máte klienta, který rozumí AtomPub, může klient preferovat tento formát přes JSON.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-254">However, if you have a client that understands AtomPub, the client might prefer that format over JSON.</span></span>

<span data-ttu-id="7b4d0-255">Tady je verze Light v rámci formátu JSON stejné entity:</span><span class="sxs-lookup"><span data-stu-id="7b4d0-255">Here is the JSON light version of the same entity:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample14.cmd)]

<span data-ttu-id="7b4d0-256">Světlý formát JSON byl představen ve verzi 3 protokolu OData.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-256">The JSON light format was introduced in version 3 of the OData protocol.</span></span> <span data-ttu-id="7b4d0-257">Z důvodu zpětné kompatibility může klient požádat o starší formát JSON "Verbose".</span><span class="sxs-lookup"><span data-stu-id="7b4d0-257">For backward compatibility, a client can request the older "verbose" JSON format.</span></span> <span data-ttu-id="7b4d0-258">Pokud chcete požádat o podrobný formát JSON, nastavte hlavičku Accept na `application/json;odata=verbose`.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-258">To request verbose JSON, set the Accept header to `application/json;odata=verbose`.</span></span> <span data-ttu-id="7b4d0-259">Zde je podrobná verze:</span><span class="sxs-lookup"><span data-stu-id="7b4d0-259">Here is the verbose version:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample15.cmd)]

<span data-ttu-id="7b4d0-260">V tomto formátu jsou další metadata v těle odpovědi, což může výrazně prodloužit nároky na celou relaci.</span><span class="sxs-lookup"><span data-stu-id="7b4d0-260">This format conveys more metadata in the response body, which can add considerable overhead over an entire session.</span></span> <span data-ttu-id="7b4d0-261">Také přidá úroveň dereference po zabalení objektu ve vlastnosti s názvem "d".</span><span class="sxs-lookup"><span data-stu-id="7b4d0-261">Also, it adds a level of indirection by wrapping the object in a property named "d".</span></span>

## <a name="next-steps"></a><span data-ttu-id="7b4d0-262">Další kroky</span><span class="sxs-lookup"><span data-stu-id="7b4d0-262">Next Steps</span></span>

- [<span data-ttu-id="7b4d0-263">Přidání vztahů mezi entitami</span><span class="sxs-lookup"><span data-stu-id="7b4d0-263">Add Entity Relations</span></span>](working-with-entity-relations.md)
- [<span data-ttu-id="7b4d0-264">Přidat akce OData</span><span class="sxs-lookup"><span data-stu-id="7b4d0-264">Add OData Actions</span></span>](odata-actions.md)
- [<span data-ttu-id="7b4d0-265">Volání služby OData z klienta .NET</span><span class="sxs-lookup"><span data-stu-id="7b4d0-265">Call the OData Service From a .NET Client</span></span>](calling-an-odata-service-from-a-net-client.md)
