---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-5
title: 'Část 5: Upravit formuláře a šablonování textu | Dokumentace Microsoftu'
author: jongalloway
description: V této sérii kurzů podrobně popisuje všechny kroky k vytvoření ukázkové aplikace ASP.NET MVC Music Store. Část 5 obsahuje úpravy formuláře a šablonování textu.
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 6b09413a-6d6a-425a-87c9-629f91b91b28
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-5
msc.type: authoredcontent
ms.openlocfilehash: e02e15a8955fa42692fac486dadfa426540295f7
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2019
ms.locfileid: "59387469"
---
# <a name="part-5-edit-forms-and-templating"></a><span data-ttu-id="ba038-104">Část 5: Editační formuláře a šablonování textu</span><span class="sxs-lookup"><span data-stu-id="ba038-104">Part 5: Edit Forms and Templating</span></span>

<span data-ttu-id="ba038-105">podle [Jon Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="ba038-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="ba038-106">MVC Music Store jde o kurz, který se seznámíte, podrobné postupy pro vývoj pro web pomocí ASP.NET MVC a sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ba038-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="ba038-107">Music Store MVC je jednoduché ukázku implementace úložiště prodává hudebních alb online, který implementuje správu základního webu, přihlášení uživatele a nákupního košíku funkce.</span><span class="sxs-lookup"><span data-stu-id="ba038-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>
> 
> <span data-ttu-id="ba038-108">V této sérii kurzů podrobně popisuje všechny kroky k vytvoření ukázkové aplikace ASP.NET MVC Music Store.</span><span class="sxs-lookup"><span data-stu-id="ba038-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="ba038-109">Část 5 obsahuje úpravy formuláře a šablonování textu.</span><span class="sxs-lookup"><span data-stu-id="ba038-109">Part 5 covers Edit Forms and Templating.</span></span>


<span data-ttu-id="ba038-110">V posledních kapitole jsme se načítání dat z databáze a jeho zobrazení.</span><span class="sxs-lookup"><span data-stu-id="ba038-110">In the past chapter, we were loading data from our database and displaying it.</span></span> <span data-ttu-id="ba038-111">V této kapitole jsme zároveň umožní úpravy data.</span><span class="sxs-lookup"><span data-stu-id="ba038-111">In this chapter, we'll also enable editing the data.</span></span>

## <a name="creating-the-storemanagercontroller"></a><span data-ttu-id="ba038-112">Vytváří StoreManagerController</span><span class="sxs-lookup"><span data-stu-id="ba038-112">Creating the StoreManagerController</span></span>

<span data-ttu-id="ba038-113">Budete Začneme tím, že vytvoříte nový kontroler volá **StoreManagerController**.</span><span class="sxs-lookup"><span data-stu-id="ba038-113">We'll begin by creating a new controller called **StoreManagerController**.</span></span> <span data-ttu-id="ba038-114">Pro tento kontroler jsme se využití výhod funkcí generování uživatelského rozhraní dostupných v ASP.NET MVC 3 nástroje Update.</span><span class="sxs-lookup"><span data-stu-id="ba038-114">For this controller, we will be taking advantage of the Scaffolding features available in the ASP.NET MVC 3 Tools Update.</span></span> <span data-ttu-id="ba038-115">Nastavení možností v dialogovém okně Přidat kontroler, jak je znázorněno níže.</span><span class="sxs-lookup"><span data-stu-id="ba038-115">Set the options for the Add Controller dialog as shown below.</span></span>

![](mvc-music-store-part-5/_static/image1.png)

<span data-ttu-id="ba038-116">Když kliknete na tlačítko Přidat, uvidíte, že mechanismus generování uživatelského rozhraní ASP.NET MVC 3 dělá správné množství práce za vás:</span><span class="sxs-lookup"><span data-stu-id="ba038-116">When you click the Add button, you'll see that the ASP.NET MVC 3 scaffolding mechanism does a good amount of work for you:</span></span>

- <span data-ttu-id="ba038-117">Vytvoří nový StoreManagerController s lokální proměnná Entity Framework</span><span class="sxs-lookup"><span data-stu-id="ba038-117">It creates the new StoreManagerController with a local Entity Framework variable</span></span>
- <span data-ttu-id="ba038-118">Přidá do zobrazení složky projektu StoreManager složku</span><span class="sxs-lookup"><span data-stu-id="ba038-118">It adds a StoreManager folder to the project's Views folder</span></span>
- <span data-ttu-id="ba038-119">Přidá zobrazení Create.cshtml, Delete.cshtml, Details.cshtml, Edit.cshtml a Index.cshtml do alb třídy silného typu</span><span class="sxs-lookup"><span data-stu-id="ba038-119">It adds Create.cshtml, Delete.cshtml, Details.cshtml, Edit.cshtml, and Index.cshtml view, strongly typed to the Album class</span></span>

![](mvc-music-store-part-5/_static/image2.png)

<span data-ttu-id="ba038-120">Nová třída kontroleru StoreManager zahrnuje CRUD (vytváření, čtení, aktualizace nebo odstranění) akce kontroleru, které už víte, jak pracovat s alba třída modelu a používat náš kontext Entity Framework pro přístup k databázi.</span><span class="sxs-lookup"><span data-stu-id="ba038-120">The new StoreManager controller class includes CRUD (create, read, update, delete) controller actions which know how to work with the Album model class and use our Entity Framework context for database access.</span></span>

## <a name="modifying-a-scaffolded-view"></a><span data-ttu-id="ba038-121">Úprava vygenerovaná zobrazení</span><span class="sxs-lookup"><span data-stu-id="ba038-121">Modifying a Scaffolded View</span></span>

<span data-ttu-id="ba038-122">Je dobré si uvědomit, že když tento kód byl generován pro nás, je standardní kód technologie ASP.NET MVC, stejně jako My jsme byl zápis v celém tomto kurzu.</span><span class="sxs-lookup"><span data-stu-id="ba038-122">It's important to remember that, while this code was generated for us, it's standard ASP.NET MVC code, just like we've been writing throughout this tutorial.</span></span> <span data-ttu-id="ba038-123">Je určená a ušetřete čas strávený by na psaní kódu kontroleru standardizované a ruční vytvoření zobrazení se silnými typy, ale to není typ generovaného kódu jste možná viděli začíná v komentářích, o jak nesmí změnit adresář upozornění kód.</span><span class="sxs-lookup"><span data-stu-id="ba038-123">It's intended to save you the time you'd spend on writing boilerplate controller code and creating the strongly typed views manually, but this isn't the kind of generated code you may have seen prefaced with dire warnings in comments about how you mustn't change the code.</span></span> <span data-ttu-id="ba038-124">To je váš kód a už má ho změnit.</span><span class="sxs-lookup"><span data-stu-id="ba038-124">This is your code, and you're expected to change it.</span></span>

<span data-ttu-id="ba038-125">Takže začneme rychlé úpravy zobrazení indexu StoreManager (/ Views/StoreManager/Index.cshtml).</span><span class="sxs-lookup"><span data-stu-id="ba038-125">So, let's start with a quick edit to the StoreManager Index view (/Views/StoreManager/Index.cshtml).</span></span> <span data-ttu-id="ba038-126">Toto zobrazení zobrazí tabulku, která obsahuje seznam alb v našem úložišti pomocí operace upravit / podrobnosti / odstranit odkazy a zahrnuje alba veřejné vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="ba038-126">This view will display a table which lists the Albums in our store with Edit / Details / Delete links, and includes the Album's public properties.</span></span> <span data-ttu-id="ba038-127">Pole AlbumArtUrl Odebereme, protože není v tomto zobrazení velmi užitečné.</span><span class="sxs-lookup"><span data-stu-id="ba038-127">We'll remove the AlbumArtUrl field, as it's not very useful in this display.</span></span> <span data-ttu-id="ba038-128">V &lt;tabulky&gt; části zobrazení kódu, odeberte &lt;th&gt; a &lt;td&gt; prvky okolní AlbumArtUrl odkazy, jak je uvedeno ve níže zvýrazněné řádky:</span><span class="sxs-lookup"><span data-stu-id="ba038-128">In &lt;table&gt; section of the view code, remove the &lt;th&gt; and &lt;td&gt; elements surrounding AlbumArtUrl references, as indicated by the highlighted lines below:</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample1.cshtml)]

<span data-ttu-id="ba038-129">Upravené zobrazit kód bude vypadat následovně:</span><span class="sxs-lookup"><span data-stu-id="ba038-129">The modified view code will appear as follows:</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample2.cshtml)]

## <a name="a-first-look-at-the-store-manager"></a><span data-ttu-id="ba038-130">První pohled na Store správce</span><span class="sxs-lookup"><span data-stu-id="ba038-130">A first look at the Store Manager</span></span>

<span data-ttu-id="ba038-131">Nyní spusťte aplikaci a přejděte do/StoreManager /.</span><span class="sxs-lookup"><span data-stu-id="ba038-131">Now run the application and browse to /StoreManager/.</span></span> <span data-ttu-id="ba038-132">Zobrazí se správce Index Store jsme právě upravili, seznamem alba v úložišti s odkazy na podrobnosti, upravit nebo odebrat.</span><span class="sxs-lookup"><span data-stu-id="ba038-132">This displays the Store Manager Index we just modified, showing a list of the albums in the store with links to Edit, Details, and Delete.</span></span>

![](mvc-music-store-part-5/_static/image3.png)

<span data-ttu-id="ba038-133">Kliknutím na odkaz pro úpravy zobrazí formulář pro úpravy s poli alba, včetně rozevírací seznamy pro žánr a interpreta.</span><span class="sxs-lookup"><span data-stu-id="ba038-133">Clicking the Edit link displays an edit form with fields for the Album, including dropdowns for Genre and Artist.</span></span>

![](mvc-music-store-part-5/_static/image4.png)

<span data-ttu-id="ba038-134">Klikněte na odkaz "Zpět do seznamu" v dolní části a potom klikněte na odkaz podrobnosti pro alba.</span><span class="sxs-lookup"><span data-stu-id="ba038-134">Click the "Back to List" link at the bottom, then click on the Details link for an Album.</span></span> <span data-ttu-id="ba038-135">Zobrazí podrobné informace o jednotlivých Album.</span><span class="sxs-lookup"><span data-stu-id="ba038-135">This displays the detail information for an individual Album.</span></span>

![](mvc-music-store-part-5/_static/image5.png)

<span data-ttu-id="ba038-136">Znovu klikněte na tlačítko Zpět na odkaz na seznamu a potom klikněte na odkaz pro odstranění.</span><span class="sxs-lookup"><span data-stu-id="ba038-136">Again, click the Back to List link, then click on a Delete link.</span></span> <span data-ttu-id="ba038-137">Zobrazí se potvrzovací dialogové okno, zobrazující podrobnosti alba a s dotazem, pokud jsme si jisti, že chceme, aby k jeho odstranění.</span><span class="sxs-lookup"><span data-stu-id="ba038-137">This displays a confirmation dialog, showing the album details and asking if we're sure we want to delete it.</span></span>

![](mvc-music-store-part-5/_static/image6.png)

<span data-ttu-id="ba038-138">Kliknutím na tlačítko Odstranit v dolní části odstranit alba a vrátí na indexovou stránku, která zobrazuje alba odstraněn.</span><span class="sxs-lookup"><span data-stu-id="ba038-138">Clicking the Delete button at the bottom will delete the album and return you to the Index page, which shows the album deleted.</span></span>

<span data-ttu-id="ba038-139">Pomocí Správce Store nezvládli jsme, ale máme řadič a zobrazit kód pro spuštění z operace CRUD.</span><span class="sxs-lookup"><span data-stu-id="ba038-139">We're not done with the Store Manager, but we have working controller and view code for the CRUD operations to start from.</span></span>

## <a name="looking-at-the-store-manager-controller-code"></a><span data-ttu-id="ba038-140">Prohlížení kódu Store správce Kontroleru</span><span class="sxs-lookup"><span data-stu-id="ba038-140">Looking at the Store Manager Controller code</span></span>

<span data-ttu-id="ba038-141">Správce řadiče Store obsahuje správné množství kódu.</span><span class="sxs-lookup"><span data-stu-id="ba038-141">The Store Manager Controller contains a good amount of code.</span></span> <span data-ttu-id="ba038-142">Podívejme to shora dolů.</span><span class="sxs-lookup"><span data-stu-id="ba038-142">Let's go through this from top to bottom.</span></span> <span data-ttu-id="ba038-143">Kontroler zahrnuje některé standardní obory názvů pro kontroler MVC, stejně jako odkaz na našem oboru názvů modelů.</span><span class="sxs-lookup"><span data-stu-id="ba038-143">The controller includes some standard namespaces for an MVC controller, as well as a reference to our Models namespace.</span></span> <span data-ttu-id="ba038-144">Kontroler má privátní instanci MusicStoreEntities používaný jednotlivými akce kontroleru pro přístup k datům.</span><span class="sxs-lookup"><span data-stu-id="ba038-144">The controller has a private instance of MusicStoreEntities, used by each of the controller actions for data access.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample3.cs)]

### <a name="store-manager-index-and-details-actions"></a><span data-ttu-id="ba038-145">Store správce Index a podrobnosti akce</span><span class="sxs-lookup"><span data-stu-id="ba038-145">Store Manager Index and Details actions</span></span>

<span data-ttu-id="ba038-146">Index zobrazení načte seznam alb, včetně každé album odkazované žánr a interpreta informace, jak jsme viděli dříve při práci na metodu Store Procházet.</span><span class="sxs-lookup"><span data-stu-id="ba038-146">The index view retrieves a list of Albums, including each album's referenced Genre and Artist information, as we previously saw when working on the Store Browse method.</span></span> <span data-ttu-id="ba038-147">Zobrazení indexu je následující odkazy na propojené objekty tak, aby ji můžete zobrazit název žánr každý alba a interpret, tak kontroleru se ještě efektivní a dotazování pro tuto informaci v původní požadavek.</span><span class="sxs-lookup"><span data-stu-id="ba038-147">The Index view is following the references to the linked objects so that it can display each album's Genre name and Artist name, so the controller is being efficient and querying for this information in the original request.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample4.cs)]

<span data-ttu-id="ba038-148">Akce kontroleru podrobnosti o adaptéru StoreManager funguje stejně jako akce Kontroleru Details Store jsme napsali dříve – dotazuje na alba podle ID, pomocí metody Find(), pak jej vrátí do zobrazení.</span><span class="sxs-lookup"><span data-stu-id="ba038-148">The StoreManager Controller's Details controller action works exactly the same as the Store Controller Details action we wrote previously - it queries for the Album by ID using the Find() method, then returns it to the view.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample5.cs)]

### <a name="the-create-action-methods"></a><span data-ttu-id="ba038-149">Vytvořit metody akce</span><span class="sxs-lookup"><span data-stu-id="ba038-149">The Create Action Methods</span></span>

<span data-ttu-id="ba038-150">Vytvořit metody akce jsou mírně liší od těch, které jsme zatím viděli, protože vstup formuláře, které zpracovávají.</span><span class="sxs-lookup"><span data-stu-id="ba038-150">The Create action methods are a little different from ones we've seen so far, because they handle form input.</span></span> <span data-ttu-id="ba038-151">Pokud uživatel nejprve navštíví /StoreManager/vytvoření /, zobrazí se prázdný formulář.</span><span class="sxs-lookup"><span data-stu-id="ba038-151">When a user first visits /StoreManager/Create/ they will be shown an empty form.</span></span> <span data-ttu-id="ba038-152">Na této stránce HTML &lt;formuláře&gt; prvků, ve kterém můžete zadat podrobnosti alba vstupní element, který obsahuje rozevírací seznam a textové pole.</span><span class="sxs-lookup"><span data-stu-id="ba038-152">This HTML page will contain a &lt;form&gt; element that contains dropdown and textbox input elements where they can enter the album's details.</span></span>

<span data-ttu-id="ba038-153">Jakmile uživatel vyplní alba hodnot formuláře, stisknutím "Save" tlačítko pro odeslání, že tyto změny zpět do naší aplikace uložte do databáze.</span><span class="sxs-lookup"><span data-stu-id="ba038-153">After the user fills in the Album form values, they can press the "Save" button to submit these changes back to our application to save within the database.</span></span> <span data-ttu-id="ba038-154">Když uživatel stiskne tlačítko "save" &lt;formuláře&gt; provede HTTP-POST zpět na /StoreManager/vytvoření/adresu URL a odešlete &lt;formuláře&gt; hodnoty jako součást požadavku HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="ba038-154">When the user presses the "save" button the &lt;form&gt; will perform an HTTP-POST back to the /StoreManager/Create/ URL and submit the &lt;form&gt; values as part of the HTTP-POST.</span></span>

<span data-ttu-id="ba038-155">ASP.NET MVC umožňuje snadno rozdělit logiku z těchto dvou scénářů volání adresy URL tím, že abychom mohli implementovat dvě samostatné metody akce "Vytvořit", v rámci naší třídy StoreManagerController – z nich se má zpracovat počáteční procházet HTTP GET /StoreManager/Create / Adresa URL a druhý pro zpracování požadavku HTTP POST odevzdané změny.</span><span class="sxs-lookup"><span data-stu-id="ba038-155">ASP.NET MVC allows us to easily split up the logic of these two URL invocation scenarios by enabling us to implement two separate "Create" action methods within our StoreManagerController class – one to handle the initial HTTP-GET browse to the /StoreManager/Create/ URL, and the other to handle the HTTP-POST of the submitted changes.</span></span>

### <a name="passing-information-to-a-view-using-viewbag"></a><span data-ttu-id="ba038-156">Předávání informací do zobrazení použití položek ViewBag</span><span class="sxs-lookup"><span data-stu-id="ba038-156">Passing information to a View using ViewBag</span></span>

<span data-ttu-id="ba038-157">Jsme využili objekt ViewBag dříve v tomto kurzu, ale nebyly mluvili většinu o něm.</span><span class="sxs-lookup"><span data-stu-id="ba038-157">We've used the ViewBag earlier in this tutorial, but haven't talked much about it.</span></span> <span data-ttu-id="ba038-158">Objekt ViewBag umožňuje k předávání informací do zobrazení bez použití objektu model silného typu.</span><span class="sxs-lookup"><span data-stu-id="ba038-158">The ViewBag allows us to pass information to the view without using a strongly typed model object.</span></span> <span data-ttu-id="ba038-159">V tomto případě naše akce kontroleru HTTP GET úpravy je potřeba předat i seznam žánry a umělci do formuláře k naplnění a nejjednodušší způsob, jak to udělat, je vrátit jako objekt ViewBag položky.</span><span class="sxs-lookup"><span data-stu-id="ba038-159">In this case, our Edit HTTP-GET controller action needs to pass both a list of Genres and Artists to the form to populate the dropdowns, and the simplest way to do that is to return them as ViewBag items.</span></span>

<span data-ttu-id="ba038-160">Objekt ViewBag je dynamický objekt, což znamená, že můžete zadat ViewBag.Foo nebo ViewBag.YourNameHere, aniž byste museli psát kód, který definuje tyto vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="ba038-160">The ViewBag is a dynamic object, meaning that you can type ViewBag.Foo or ViewBag.YourNameHere without writing code to define those properties.</span></span> <span data-ttu-id="ba038-161">Kód kontroler použije v tomto případě ViewBag.GenreId a ViewBag.ArtistId tak, aby odeslané s formuláři rozevíracího seznamu hodnoty budou GenreId a ArtistId, které jsou vlastnosti, které se nastavení.</span><span class="sxs-lookup"><span data-stu-id="ba038-161">In this case, the controller code uses ViewBag.GenreId and ViewBag.ArtistId so that the dropdown values submitted with the form will be GenreId and ArtistId, which are the Album properties they will be setting.</span></span>

<span data-ttu-id="ba038-162">Tyto hodnoty rozevírací seznam se vrátí do formuláře pomocí SelectList objektu, který je vytvořenou přesně pro tento účel.</span><span class="sxs-lookup"><span data-stu-id="ba038-162">These dropdown values are returned to the form using the SelectList object, which is built just for that purpose.</span></span> <span data-ttu-id="ba038-163">To se provádí pomocí kódu takto:</span><span class="sxs-lookup"><span data-stu-id="ba038-163">This is done using code like this:</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample6.cs)]

<span data-ttu-id="ba038-164">Jak je vidět z kódu metody akce, tři parametry jsou použity k vytvoření tohoto objektu:</span><span class="sxs-lookup"><span data-stu-id="ba038-164">As you can see from the action method code, three parameters are being used to create this object:</span></span>

- <span data-ttu-id="ba038-165">Seznam položek, které rozevírací seznam bude zobrazení.</span><span class="sxs-lookup"><span data-stu-id="ba038-165">The list of items the dropdown will be displaying.</span></span> <span data-ttu-id="ba038-166">Všimněte si, že to není jenom řetězec – jsme se předají seznam žánrů.</span><span class="sxs-lookup"><span data-stu-id="ba038-166">Note that this isn't just a string - we're passing a list of Genres.</span></span>
- <span data-ttu-id="ba038-167">Další parametr předávaný do SelectList je vybraná hodnota.</span><span class="sxs-lookup"><span data-stu-id="ba038-167">The next parameter being passed to the SelectList is the Selected Value.</span></span> <span data-ttu-id="ba038-168">Tento způsob SelectList ví, jak předem vyberete položku v seznamu.</span><span class="sxs-lookup"><span data-stu-id="ba038-168">This how the SelectList knows how to pre-select an item in the list.</span></span> <span data-ttu-id="ba038-169">To bude srozumitelnější, když se podíváme na formulář pro úpravy, které je hodně podobné.</span><span class="sxs-lookup"><span data-stu-id="ba038-169">This will be easier to understand when we look at the Edit form, which is pretty similar.</span></span>
- <span data-ttu-id="ba038-170">Poslední parametr je vlastnost, která má být zobrazena.</span><span class="sxs-lookup"><span data-stu-id="ba038-170">The final parameter is the property to be displayed.</span></span> <span data-ttu-id="ba038-171">V tomto případě to je, že vlastnost Genre.Name co se zobrazí uživateli.</span><span class="sxs-lookup"><span data-stu-id="ba038-171">In this case, this is indicating that the Genre.Name property is what will be shown to the user.</span></span>

<span data-ttu-id="ba038-172">To na paměti pak je docela jednoduché akce HTTP GET vytvoření – dva SelectLists jsou přidány do objekt ViewBag a žádný objekt modelu je předán do formuláře (protože nebyl ještě vytvořen).</span><span class="sxs-lookup"><span data-stu-id="ba038-172">With that in mind, then, the HTTP-GET Create action is pretty simple - two SelectLists are added to the ViewBag, and no model object is passed to the form (since it hasn't been created yet).</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample7.cs)]

### <a name="html-helpers-to-display-the-drop-downs-in-the-create-view"></a><span data-ttu-id="ba038-173">Pomocné rutiny HTML zobrazíte rozevírací nabídky v zobrazení pro vytváření</span><span class="sxs-lookup"><span data-stu-id="ba038-173">HTML Helpers to display the Drop Downs in the Create View</span></span>

<span data-ttu-id="ba038-174">Vzhledem k tomu, že už jsme mluvili o jak rozevírací seznam hodnot jsou předány do zobrazení, Pojďme se na rychlý pohled na zobrazení, abyste viděli, jak tyto hodnoty jsou zobrazeny.</span><span class="sxs-lookup"><span data-stu-id="ba038-174">Since we've talked about how the drop down values are passed to the view, let's take a quick look at the view to see how those values are displayed.</span></span> <span data-ttu-id="ba038-175">V zobrazení kódu (/ Views/StoreManager/Create.cshtml), zobrazí se následující při volání k zobrazení seznamu žánr dolů.</span><span class="sxs-lookup"><span data-stu-id="ba038-175">In the view code (/Views/StoreManager/Create.cshtml), you'll see the following call is made to display the Genre drop down.</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample8.cshtml)]

<span data-ttu-id="ba038-176">To se označuje jako pomocné rutiny HTML – nástroj pro metodu, která provádí běžné zobrazení úlohy.</span><span class="sxs-lookup"><span data-stu-id="ba038-176">This is known as an HTML Helper - a utility method which performs a common view task.</span></span> <span data-ttu-id="ba038-177">Pomocné rutiny HTML jsou velmi užitečné při zachování našeho kódu zobrazení stručnější a čitelnější.</span><span class="sxs-lookup"><span data-stu-id="ba038-177">HTML Helpers are very useful in keeping our view code concise and readable.</span></span> <span data-ttu-id="ba038-178">Poskytuje pomocné rutiny Html.DropDownList ASP.NET MVC, ale jak uvidíme dále je možné vytvořit vlastní pomocné rutiny pro zobrazení kódu, které nám budete znovu použít v naší aplikaci.</span><span class="sxs-lookup"><span data-stu-id="ba038-178">The Html.DropDownList helper is provided by ASP.NET MVC, but as we'll see later it's possible to create our own helpers for view code we'll reuse in our application.</span></span>

<span data-ttu-id="ba038-179">Volání Html.DropDownList je jenom nutné až k tomu dojde dvě věci – tam, kde k získání seznamu zobrazíte a jakou hodnotu (pokud existuje) musí být předem vybraná.</span><span class="sxs-lookup"><span data-stu-id="ba038-179">The Html.DropDownList call just needs to be told two things - where to get the list to display, and what value (if any) should be pre-selected.</span></span> <span data-ttu-id="ba038-180">První parametr GenreId, říká DropDownList hledat hodnotu s názvem GenreId v modelu nebo objekt ViewBag.</span><span class="sxs-lookup"><span data-stu-id="ba038-180">The first parameter, GenreId, tells the DropDownList to look for a value named GenreId in either the model or ViewBag.</span></span> <span data-ttu-id="ba038-181">Druhý parametr slouží k označení hodnoty zobrazíte původně vybrali v rozevíracím seznamu.</span><span class="sxs-lookup"><span data-stu-id="ba038-181">The second parameter is used to indicate the value to show as initially selected in the drop down list.</span></span> <span data-ttu-id="ba038-182">Protože tento formulář je formulář pro vytvoření, neexistuje žádná hodnota bude Zkontrolujte předem vybrané a je předán String.Empty.</span><span class="sxs-lookup"><span data-stu-id="ba038-182">Since this form is a Create form, there's no value to be preselected and String.Empty is passed.</span></span>

### <a name="handling-the-posted-form-values"></a><span data-ttu-id="ba038-183">Zpracování hodnot publikování formuláře</span><span class="sxs-lookup"><span data-stu-id="ba038-183">Handling the Posted Form values</span></span>

<span data-ttu-id="ba038-184">Jak jsme probírali před, existují dvě metody akce přidružené každý formulář.</span><span class="sxs-lookup"><span data-stu-id="ba038-184">As we discussed before, there are two action methods associated with each form.</span></span> <span data-ttu-id="ba038-185">První zpracuje požadavek HTTP GET a zobrazí formulář.</span><span class="sxs-lookup"><span data-stu-id="ba038-185">The first handles the HTTP-GET request and displays the form.</span></span> <span data-ttu-id="ba038-186">Druhá zpracovává žádost HTTP POST, který obsahuje hodnoty odeslané formuláře.</span><span class="sxs-lookup"><span data-stu-id="ba038-186">The second handles the HTTP-POST request, which contains the submitted form values.</span></span> <span data-ttu-id="ba038-187">Všimněte si, že má akce kontroleru atributu [HttpPost], který technologii ASP.NET MVC řekne, že by měl pouze reagovat na požadavky HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="ba038-187">Notice that controller action has an [HttpPost] attribute, which tells ASP.NET MVC that it should only respond to HTTP-POST requests.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample9.cs)]

<span data-ttu-id="ba038-188">Tato akce má čtyři odpovědnosti:</span><span class="sxs-lookup"><span data-stu-id="ba038-188">This action has four responsibilities:</span></span>

- 1. <span data-ttu-id="ba038-189">Čtení hodnot formuláře</span><span class="sxs-lookup"><span data-stu-id="ba038-189">Read the form values</span></span>
- 2. <span data-ttu-id="ba038-190">Zaškrtněte, pokud hodnot formuláře předejte všechna pravidla ověřování</span><span class="sxs-lookup"><span data-stu-id="ba038-190">Check if the form values pass any validation rules</span></span>
- 3. <span data-ttu-id="ba038-191">Pokud se odeslání formuláře je platný, uložit data a zobrazí aktualizovaný seznam</span><span class="sxs-lookup"><span data-stu-id="ba038-191">If the form submission is valid, save the data and display the updated list</span></span>
- 4. <span data-ttu-id="ba038-192">Pokud odeslání formuláře není platná, znovu zobrazte formulář s chyby ověření</span><span class="sxs-lookup"><span data-stu-id="ba038-192">If the form submission is not valid, redisplay the form with validation errors</span></span>

#### <a name="reading-form-values-with-model-binding"></a><span data-ttu-id="ba038-193">Čtení hodnot formuláře pomocí vazby modelu</span><span class="sxs-lookup"><span data-stu-id="ba038-193">Reading Form Values with Model Binding</span></span>

<span data-ttu-id="ba038-194">Odeslání formuláře, který obsahuje hodnoty GenreId a ArtistId (z rozevíracího seznamu) a textové pole hodnot pro název, cena a AlbumArtUrl zpracovává akce kontroleru.</span><span class="sxs-lookup"><span data-stu-id="ba038-194">The controller action is processing a form submission that includes values for GenreId and ArtistId (from the drop down list) and textbox values for Title, Price, and AlbumArtUrl.</span></span> <span data-ttu-id="ba038-195">I když je možné pro přímý přístup k hodnotám formuláře, lepším řešením je použití do ASP.NET MVC integrované možnosti vazby modelu.</span><span class="sxs-lookup"><span data-stu-id="ba038-195">While it's possible to directly access form values, a better approach is to use the Model Binding capabilities built into ASP.NET MVC.</span></span> <span data-ttu-id="ba038-196">Typ modelu, který jako parametr pořízením akce kontroleru ASP.NET MVC se pokusí o naplnění objektu tohoto typu pomocí formuláře vstupy (stejně jako hodnoty trasy a řetězce dotazu).</span><span class="sxs-lookup"><span data-stu-id="ba038-196">When a controller action takes a model type as a parameter, ASP.NET MVC will attempt to populate an object of that type using form inputs (as well as route and querystring values).</span></span> <span data-ttu-id="ba038-197">Dělá to pomocí hodnot, jejichž názvy odpovídají vlastností objektu modelu, třeba při nastavování hodnoty GenreId nový objekt alb, hledá vstupní hodnota s názvem GenreId.</span><span class="sxs-lookup"><span data-stu-id="ba038-197">It does this by looking for values whose names match properties of the model object, e.g. when setting the new Album object's GenreId value, it looks for an input with the name GenreId.</span></span> <span data-ttu-id="ba038-198">Při vytváření zobrazení pomocí standardních metod v architektuře ASP.NET MVC formuláře bude vždy být vykreslen pomocí názvy vlastností jako názvy vstupních polí, takže to názvy polí se právě spárujte.</span><span class="sxs-lookup"><span data-stu-id="ba038-198">When you create views using the standard methods in ASP.NET MVC, the forms will always be rendered using property names as input field names, so this the field names will just match up.</span></span>

#### <a name="validating-the-model"></a><span data-ttu-id="ba038-199">Ověření modelu</span><span class="sxs-lookup"><span data-stu-id="ba038-199">Validating the Model</span></span>

<span data-ttu-id="ba038-200">Model se ověří pomocí jednoduchého volání do ModelState.IsValid.</span><span class="sxs-lookup"><span data-stu-id="ba038-200">The model is validated with a simple call to ModelState.IsValid.</span></span> <span data-ttu-id="ba038-201">Jsme nepřidali žádná pravidla ověřování do naší třídy alba ještě – uděláme, které se za chvilku – teď tuto kontrolu nemusí dělat v podstatě.</span><span class="sxs-lookup"><span data-stu-id="ba038-201">We haven't added any validation rules to our Album class yet - we'll do that in a bit - so right now this check doesn't have much to do.</span></span> <span data-ttu-id="ba038-202">Důležité je, že tato kontrola ModelStat.IsValid se bude přizpůsobovat ověřovacích pravidel, které jsme na náš model, takže budoucí změny pravidel ověřování nevyžadují žádné aktualizace kódu akce kontroleru.</span><span class="sxs-lookup"><span data-stu-id="ba038-202">What's important is that this ModelStat.IsValid check will adapt to the validation rules we put on our model, so future changes to validation rules won't require any updates to the controller action code.</span></span>

#### <a name="saving-the-submitted-values"></a><span data-ttu-id="ba038-203">Ukládá zadané hodnoty</span><span class="sxs-lookup"><span data-stu-id="ba038-203">Saving the submitted values</span></span>

<span data-ttu-id="ba038-204">Pokud odeslání formuláře projdou ověřením, je čas k uložení hodnoty do databáze.</span><span class="sxs-lookup"><span data-stu-id="ba038-204">If the form submission passes validation, it's time to save the values to the database.</span></span> <span data-ttu-id="ba038-205">S Entity Framework, která vyžaduje jen přidáním modelu do kolekce alba a volání SaveChanges.</span><span class="sxs-lookup"><span data-stu-id="ba038-205">With Entity Framework, that just requires adding the model to the Albums collection and calling SaveChanges.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample10.cs)]

<span data-ttu-id="ba038-206">Entity Framework generuje příslušnými příkazy SQL pro uchování hodnoty.</span><span class="sxs-lookup"><span data-stu-id="ba038-206">Entity Framework generates the appropriate SQL commands to persist the value.</span></span> <span data-ttu-id="ba038-207">Po uložení dat, jsme přesměrovat zpět do seznamu alb, takže uvidíme náš aktualizace.</span><span class="sxs-lookup"><span data-stu-id="ba038-207">After saving the data, we redirect back to the list of Albums so we can see our update.</span></span> <span data-ttu-id="ba038-208">To se provádí tak, že vrací RedirectToAction s názvem, které chceme zobrazená akce kontroleru.</span><span class="sxs-lookup"><span data-stu-id="ba038-208">This is done by returning RedirectToAction with the name of the controller action we want displayed.</span></span> <span data-ttu-id="ba038-209">V tomto případě to je metoda Index.</span><span class="sxs-lookup"><span data-stu-id="ba038-209">In this case, that's the Index method.</span></span>

#### <a name="displaying-invalid-form-submissions-with-validation-errors"></a><span data-ttu-id="ba038-210">Neplatná notace odesílání chyb ověření zobrazení</span><span class="sxs-lookup"><span data-stu-id="ba038-210">Displaying invalid form submissions with Validation Errors</span></span>

<span data-ttu-id="ba038-211">V případě neplatná notace vstupní hodnoty rozevírací seznam se přidají do objekt ViewBag (stejně jako v případě protokolu HTTP GET) a hodnoty vazby modelu jsou předány zpět do zobrazení pro zobrazení.</span><span class="sxs-lookup"><span data-stu-id="ba038-211">In the case of invalid form input, the dropdown values are added to the ViewBag (as in the HTTP-GET case) and the bound model values are passed back to the view for display.</span></span> <span data-ttu-id="ba038-212">Chyby ověřování se automaticky zobrazí pomocí @Html.ValidationMessageFor pomocné rutiny HTML.</span><span class="sxs-lookup"><span data-stu-id="ba038-212">Validation errors are automatically displayed using the @Html.ValidationMessageFor HTML Helper.</span></span>

#### <a name="testing-the-create-form"></a><span data-ttu-id="ba038-213">Testování vytvořit formulář</span><span class="sxs-lookup"><span data-stu-id="ba038-213">Testing the Create Form</span></span>

<span data-ttu-id="ba038-214">K otestování to, spusťte aplikaci a přejděte na /StoreManager/vytvoření / – zobrazí se prázdný formulář, který byl vrácen metodou HTTP pro vytvoření StoreController-GET.</span><span class="sxs-lookup"><span data-stu-id="ba038-214">To test this out, run the application and browse to /StoreManager/Create/ - this will show you the blank form which was returned by the StoreController Create HTTP-GET method.</span></span>

<span data-ttu-id="ba038-215">Vyplňte hodnoty a klikněte na tlačítko Vytvořit k odeslání formuláře.</span><span class="sxs-lookup"><span data-stu-id="ba038-215">Fill in some values and click the Create button to submit the form.</span></span>

![](mvc-music-store-part-5/_static/image7.png)

![](mvc-music-store-part-5/_static/image8.png)

### <a name="handling-edits"></a><span data-ttu-id="ba038-216">Zpracování úprav</span><span class="sxs-lookup"><span data-stu-id="ba038-216">Handling Edits</span></span>

<span data-ttu-id="ba038-217">Jsou velmi podobné vytvořit metody akce, které zvažovali jsme i jen pár akce úpravy (HTTP GET a POST protokolu HTTP).</span><span class="sxs-lookup"><span data-stu-id="ba038-217">The Edit action pair (HTTP-GET and HTTP-POST) are very similar to the Create action methods we just looked at.</span></span> <span data-ttu-id="ba038-218">Protože Upravit scénář zahrnuje práce s existující album, upravit HTTP-GET načte metoda na základě parametru "id" Album předaný prostřednictvím trasy.</span><span class="sxs-lookup"><span data-stu-id="ba038-218">Since the edit scenario involves working with an existing album, the Edit HTTP-GET method loads the Album based on the "id" parameter, passed in via the route.</span></span> <span data-ttu-id="ba038-219">Tento kód pro načtení alba podle AlbumId je stejný, jako jsme dříve se zabývali v podrobnosti akce kontroleru.</span><span class="sxs-lookup"><span data-stu-id="ba038-219">This code for retrieving an album by AlbumId is the same as we've previously looked at in the Details controller action.</span></span> <span data-ttu-id="ba038-220">Stejně jako u vytvořením / metody GET protokolu HTTP, rozevírací seznam hodnot jsou vráceny prostřednictvím objekt ViewBag.</span><span class="sxs-lookup"><span data-stu-id="ba038-220">As with the Create / HTTP-GET method, the drop down values are returned via the ViewBag.</span></span> <span data-ttu-id="ba038-221">To umožňuje vrátit alba jako náš model objektu zobrazení (které je silně typováno do třídy alba) při předání dalších dat (např. seznam žánry) přes objekt ViewBag.</span><span class="sxs-lookup"><span data-stu-id="ba038-221">This allows us to return an Album as our model object to the view (which is strongly typed to the Album class) while passing additional data (e.g. a list of Genres) via the ViewBag.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample11.cs)]

<span data-ttu-id="ba038-222">Upravit HTTP-POST akce je velmi podobný akce vytvoření HTTP-POST.</span><span class="sxs-lookup"><span data-stu-id="ba038-222">The Edit HTTP-POST action is very similar to the Create HTTP-POST action.</span></span> <span data-ttu-id="ba038-223">Jediným rozdílem je, že místo přidání nové album k databázi. Kolekce alb, jsme hledáte aktuální instance alba pomocí databáze. Entry(album) a nastavení jeho stavu na změněné.</span><span class="sxs-lookup"><span data-stu-id="ba038-223">The only difference is that instead of adding a new album to the db.Albums collection, we're finding the current instance of the Album using db.Entry(album) and setting its state to Modified.</span></span> <span data-ttu-id="ba038-224">To říká Entity Framework, upravovat stávající album na rozdíl od vytvoření nového.</span><span class="sxs-lookup"><span data-stu-id="ba038-224">This tells Entity Framework that we are modifying an existing album as opposed to creating a new one.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample12.cs)]

<span data-ttu-id="ba038-225">Můžeme to zjistit otestovat spuštění aplikace a přejdete do/StoreManger/a poté kliknutím na odkaz pro úpravy pro alba.</span><span class="sxs-lookup"><span data-stu-id="ba038-225">We can test this out by running the application and browsing to /StoreManger/, then clicking the Edit link for an album.</span></span>

![](mvc-music-store-part-5/_static/image9.png)

<span data-ttu-id="ba038-226">Zobrazí se zobrazí metodou HTTP GET upravit formulář pro úpravy.</span><span class="sxs-lookup"><span data-stu-id="ba038-226">This displays the Edit form shown by the Edit HTTP-GET method.</span></span> <span data-ttu-id="ba038-227">Vyplňte hodnoty a klikněte na tlačítko Uložit.</span><span class="sxs-lookup"><span data-stu-id="ba038-227">Fill in some values and click the Save button.</span></span>

![](mvc-music-store-part-5/_static/image10.png)

<span data-ttu-id="ba038-228">To formulář odešle, uloží hodnoty a vrátí nám do seznamu obrázek znázorňující, že hodnoty byly aktualizovány.</span><span class="sxs-lookup"><span data-stu-id="ba038-228">This posts the form, saves the values, and returns us to the Album list, showing that the values were updated.</span></span>

![](mvc-music-store-part-5/_static/image11.png)

### <a name="handling-deletion"></a><span data-ttu-id="ba038-229">Zpracování odstranění</span><span class="sxs-lookup"><span data-stu-id="ba038-229">Handling Deletion</span></span>

<span data-ttu-id="ba038-230">Odstranění používá stejný vzor jako Edit and Create, pomocí akce jeden kontroler k potvrzení formulář pro zobrazení a další akce kontroleru pro zpracování odeslání formuláře.</span><span class="sxs-lookup"><span data-stu-id="ba038-230">Deletion follows the same pattern as Edit and Create, using one controller action to display the confirmation form, and another controller action to handle the form submission.</span></span>

<span data-ttu-id="ba038-231">Akce kontroleru HTTP GET odstranit je přesně stejný jako naše předchozí akce kontroleru Store správce podrobnosti.</span><span class="sxs-lookup"><span data-stu-id="ba038-231">The HTTP-GET Delete controller action is exactly the same as our previous Store Manager Details controller action.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample13.cs)]

<span data-ttu-id="ba038-232">Formulář, který je silně typováno zobrazíme na typ alb, šablona odstranit zobrazení obsahu.</span><span class="sxs-lookup"><span data-stu-id="ba038-232">We display a form that's strongly typed to an Album type, using the Delete view content template.</span></span>

![](mvc-music-store-part-5/_static/image12.png)

<span data-ttu-id="ba038-233">Odstranit šablonu zobrazí všechna pole pro model, ale můžeme odlišují zjednodušit tohoto seznamu.</span><span class="sxs-lookup"><span data-stu-id="ba038-233">The Delete template shows all the fields for the model, but we can simplify that down quite a bit.</span></span> <span data-ttu-id="ba038-234">Změňte zobrazení kódu v /Views/StoreManager/Delete.cshtml takto.</span><span class="sxs-lookup"><span data-stu-id="ba038-234">Change the view code in /Views/StoreManager/Delete.cshtml to the following.</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample14.cshtml)]

<span data-ttu-id="ba038-235">Zobrazí se zjednodušený potvrzení odstranění.</span><span class="sxs-lookup"><span data-stu-id="ba038-235">This displays a simplified Delete confirmation.</span></span>

![](mvc-music-store-part-5/_static/image13.png)

<span data-ttu-id="ba038-236">Kliknutím na tlačítko Odstranit způsobí, že formulář, který se má publikovat zpět na server, který provede akci DeleteConfirmed.</span><span class="sxs-lookup"><span data-stu-id="ba038-236">Clicking the Delete button causes the form to be posted back to the server, which executes the DeleteConfirmed action.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample15.cs)]

<span data-ttu-id="ba038-237">Naše HTTP POST odstranit akce Kontroleru provede následující akce:</span><span class="sxs-lookup"><span data-stu-id="ba038-237">Our HTTP-POST Delete Controller Action takes the following actions:</span></span>

- 1. <span data-ttu-id="ba038-238">Načte alba podle ID</span><span class="sxs-lookup"><span data-stu-id="ba038-238">Loads the Album by ID</span></span>
- 2. <span data-ttu-id="ba038-239">Neodstraní alba a uložit změny</span><span class="sxs-lookup"><span data-stu-id="ba038-239">Deletes it the album and save changes</span></span>
- 3. <span data-ttu-id="ba038-240">Provede přesměrování Index, zobrazuje, zda alba byl odebrán ze seznamu</span><span class="sxs-lookup"><span data-stu-id="ba038-240">Redirects to the Index, showing that the Album was removed from the list</span></span>

<span data-ttu-id="ba038-241">Abyste to mohli otestovat, spusťte aplikaci a přejděte do /StoreManager.</span><span class="sxs-lookup"><span data-stu-id="ba038-241">To test this, run the application and browse to /StoreManager.</span></span> <span data-ttu-id="ba038-242">Vyberte alba ze seznamu a klikněte na odkaz pro odstranění.</span><span class="sxs-lookup"><span data-stu-id="ba038-242">Select an album from the list and click the Delete link.</span></span>

![](mvc-music-store-part-5/_static/image14.png)

<span data-ttu-id="ba038-243">Zobrazí se potvrzovací obrazovce a naše odstranit.</span><span class="sxs-lookup"><span data-stu-id="ba038-243">This displays our Delete confirmation screen.</span></span>

![](mvc-music-store-part-5/_static/image15.png)

<span data-ttu-id="ba038-244">Kliknutím na tlačítko Odstranit odebere alba a vrátí nám na Store správce indexovou stránku, který ukazuje, že alba byl odstraněn.</span><span class="sxs-lookup"><span data-stu-id="ba038-244">Clicking the Delete button removes the album and returns us to the Store Manager Index page, which shows that the album has been deleted.</span></span>

![](mvc-music-store-part-5/_static/image16.png)

### <a name="using-a-custom-html-helper-to-truncate-text"></a><span data-ttu-id="ba038-245">Použití vlastní pomocné rutiny HTML došlo ke zkrácení text</span><span class="sxs-lookup"><span data-stu-id="ba038-245">Using a custom HTML Helper to truncate text</span></span>

<span data-ttu-id="ba038-246">Máme jedním potenciálním problémem s naší Store správce indexovou stránku.</span><span class="sxs-lookup"><span data-stu-id="ba038-246">We've got one potential issue with our Store Manager Index page.</span></span> <span data-ttu-id="ba038-247">Naše alba a interpret vlastnosti mohou být dostatečně dlouhá, že může vyvolat vypnout naše formátování tabulky.</span><span class="sxs-lookup"><span data-stu-id="ba038-247">Our Album Title and Artist Name properties can both be long enough that they could throw off our table formatting.</span></span> <span data-ttu-id="ba038-248">Vytvoříme vlastní pomocné rutiny HTML k umožňuje snadno zkrátit těchto a dalších vlastnostech v našich zobrazení.</span><span class="sxs-lookup"><span data-stu-id="ba038-248">We'll create a custom HTML Helper to allow us to easily truncate these and other properties in our Views.</span></span>

![](mvc-music-store-part-5/_static/image17.png)

<span data-ttu-id="ba038-249">Syntaxe Razor pro @helper syntaxe bylo poměrně snadno vytvořit vlastní pomocné funkce pro použití v zobrazení.</span><span class="sxs-lookup"><span data-stu-id="ba038-249">Razor's @helper syntax has made it pretty easy to create your own helper functions for use in your views.</span></span> <span data-ttu-id="ba038-250">Otevření zobrazení /Views/StoreManager/Index.cshtml a následující kód přidejte přímo po @model řádku.</span><span class="sxs-lookup"><span data-stu-id="ba038-250">Open the /Views/StoreManager/Index.cshtml view and add the following code directly after the @model line.</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample16.cshtml)]

<span data-ttu-id="ba038-251">Tato pomocná metoda přijímá řetězec a umožňující maximální délku.</span><span class="sxs-lookup"><span data-stu-id="ba038-251">This helper method takes a string and a maximum length to allow.</span></span> <span data-ttu-id="ba038-252">Pokud zadaný text je kratší než délka zadaná, pomocné rutiny uloží jej jako-je.</span><span class="sxs-lookup"><span data-stu-id="ba038-252">If the text supplied is shorter than the length specified, the helper outputs it as-is.</span></span> <span data-ttu-id="ba038-253">Pokud je delší, zkrátí text a vykreslí "..." pro zbytek.</span><span class="sxs-lookup"><span data-stu-id="ba038-253">If it is longer, then it truncates the text and renders "…" for the remainder.</span></span>

<span data-ttu-id="ba038-254">Teď můžeme použít naše Truncate pomocné rutiny pro interpret i název vlastnosti musí být kratší než 25 znaků.</span><span class="sxs-lookup"><span data-stu-id="ba038-254">Now we can use our Truncate helper to ensure that both the Album Title and Artist Name properties are less than 25 characters.</span></span> <span data-ttu-id="ba038-255">Kompletní přehled kódu pomocí našich nových Truncate pomocné rutiny se zobrazí pod.</span><span class="sxs-lookup"><span data-stu-id="ba038-255">The complete view code using our new Truncate helper appears below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample17.cshtml)]

<span data-ttu-id="ba038-256">Nyní když jsme procházejí /StoreManager/ adresy URL, alba a názvy jsou zachovány nižší než naše maximální délky.</span><span class="sxs-lookup"><span data-stu-id="ba038-256">Now when we browse the /StoreManager/ URL, the albums and titles are kept below our maximum lengths.</span></span>

![](mvc-music-store-part-5/_static/image18.png)

<span data-ttu-id="ba038-257">Poznámka: Ukazuje jednoduchý případ vytváření a použití pomocné rutiny v jednom zobrazení.</span><span class="sxs-lookup"><span data-stu-id="ba038-257">Note: This shows the simple case of creating and using a helper in one view.</span></span> <span data-ttu-id="ba038-258">Další informace o vytvoření pomocných rutin, které můžete použít v celém webu, najdete v mé blogovém příspěvku: [http://bit.ly/mvc3-helper-options](http://bit.ly/mvc3-helper-options)</span><span class="sxs-lookup"><span data-stu-id="ba038-258">To learn more about creating helpers that you can use throughout your site, see my blog post: [http://bit.ly/mvc3-helper-options](http://bit.ly/mvc3-helper-options)</span></span>


> [!div class="step-by-step"]
> <span data-ttu-id="ba038-259">[Předchozí](mvc-music-store-part-4.md)
> [další](mvc-music-store-part-6.md)</span><span class="sxs-lookup"><span data-stu-id="ba038-259">[Previous](mvc-music-store-part-4.md)
[Next](mvc-music-store-part-6.md)</span></span>
