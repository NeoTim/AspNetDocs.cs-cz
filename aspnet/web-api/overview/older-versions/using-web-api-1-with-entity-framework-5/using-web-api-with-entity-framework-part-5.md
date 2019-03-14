---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-5
title: 'Část 5: Vytvoření dynamického uživatelského rozhraní s knihovnou Knockout.js | Dokumentace Microsoftu'
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: 9d9cb3b0-f4a7-434e-a508-9fc0ad0eb813
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-5
msc.type: authoredcontent
ms.openlocfilehash: d019941700992e173a5812b11b558b6726dfd809
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57066163"
---
<a name="part-5-creating-a-dynamic-ui-with-knockoutjs"></a><span data-ttu-id="f25ce-102">Část 5: Vytvoření dynamického uživatelského rozhraní s knihovnou Knockout.js</span><span class="sxs-lookup"><span data-stu-id="f25ce-102">Part 5: Creating a Dynamic UI with Knockout.js</span></span>
====================
<span data-ttu-id="f25ce-103">podle [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="f25ce-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="f25ce-104">Stáhnout dokončený projekt</span><span class="sxs-lookup"><span data-stu-id="f25ce-104">Download Completed Project</span></span>](http://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="creating-a-dynamic-ui-with-knockoutjs"></a><span data-ttu-id="f25ce-105">Vytvoření dynamického uživatelského rozhraní s knihovnou Knockout.js</span><span class="sxs-lookup"><span data-stu-id="f25ce-105">Creating a Dynamic UI with Knockout.js</span></span>

<span data-ttu-id="f25ce-106">V této části používáme rozhraní Knockout.js Přidání funkčnosti do zobrazení správce.</span><span class="sxs-lookup"><span data-stu-id="f25ce-106">In this section, we'll use Knockout.js to add functionality to the Admin view.</span></span>

<span data-ttu-id="f25ce-107">[Rozhraní Knockout.js](http://knockoutjs.com/) je knihovna jazyka Javascript, který usnadňuje vytvoření vazby ovládacích prvků HTML k datům.</span><span class="sxs-lookup"><span data-stu-id="f25ce-107">[Knockout.js](http://knockoutjs.com/) is a Javascript library that makes it easy to bind HTML controls to data.</span></span> <span data-ttu-id="f25ce-108">Rozhraní Knockout.js používá vzor Model-View-ViewModel (MVVM).</span><span class="sxs-lookup"><span data-stu-id="f25ce-108">Knockout.js uses the Model-View-ViewModel (MVVM) pattern.</span></span>

- <span data-ttu-id="f25ce-109">*Modelu* je reprezentace dat v obchodní domény (v našich případě produktů a objednávky) na straně serveru.</span><span class="sxs-lookup"><span data-stu-id="f25ce-109">The *model* is the server-side representation of the data in the business domain (in our case, products and orders).</span></span>
- <span data-ttu-id="f25ce-110">*Zobrazení* je prezentační vrstvy (HTML).</span><span class="sxs-lookup"><span data-stu-id="f25ce-110">The *view* is the presentation layer (HTML).</span></span>
- <span data-ttu-id="f25ce-111">*Model zobrazení* je objekt jazyka Javascript, která obsahuje data modelu.</span><span class="sxs-lookup"><span data-stu-id="f25ce-111">The *view-model* is a Javascript object that holds the model data.</span></span> <span data-ttu-id="f25ce-112">Model zobrazení je abstrakce kód uživatelského rozhraní.</span><span class="sxs-lookup"><span data-stu-id="f25ce-112">The view-model is a code abstraction of the UI.</span></span> <span data-ttu-id="f25ce-113">Nemá žádné znalosti jazyka HTML představující.</span><span class="sxs-lookup"><span data-stu-id="f25ce-113">It has no knowledge of the HTML representation.</span></span> <span data-ttu-id="f25ce-114">Místo toho představuje abstraktní funkce zobrazení, jako je například "seznam položek".</span><span class="sxs-lookup"><span data-stu-id="f25ce-114">Instead, it represents abstract features of the view, such as "a list of items".</span></span>

<span data-ttu-id="f25ce-115">Zobrazení je vázán na data modelu zobrazení.</span><span class="sxs-lookup"><span data-stu-id="f25ce-115">The view is data-bound to the view-model.</span></span> <span data-ttu-id="f25ce-116">Aktualizace zobrazení modelu se automaticky projeví v zobrazení.</span><span class="sxs-lookup"><span data-stu-id="f25ce-116">Updates to the view-model are automatically reflected in the view.</span></span> <span data-ttu-id="f25ce-117">Model zobrazení také načte události z zobrazení, jako je například kliknutí na tlačítko a provádí operace v modelu, jako je například vytvoření objednávky.</span><span class="sxs-lookup"><span data-stu-id="f25ce-117">The view-model also gets events from the view, such as button clicks, and performs operations on the model, such as creating an order.</span></span>

![](using-web-api-with-entity-framework-part-5/_static/image1.png)

<span data-ttu-id="f25ce-118">Budeme nejprve definovat model zobrazení.</span><span class="sxs-lookup"><span data-stu-id="f25ce-118">First we'll define the view-model.</span></span> <span data-ttu-id="f25ce-119">Potom jsme vytvoří vazbu modelu zobrazení bude značka jazyka HTML.</span><span class="sxs-lookup"><span data-stu-id="f25ce-119">After that, we will bind the HTML markup to the view-model.</span></span>

<span data-ttu-id="f25ce-120">Přidejte následující část Razor na Admin.cshtml:</span><span class="sxs-lookup"><span data-stu-id="f25ce-120">Add the following Razor section to Admin.cshtml:</span></span>

[!code-cshtml[Main](using-web-api-with-entity-framework-part-5/samples/sample1.cshtml)]

<span data-ttu-id="f25ce-121">V této části můžete přidat kamkoli v souboru.</span><span class="sxs-lookup"><span data-stu-id="f25ce-121">You can add this section anywhere in the file.</span></span> <span data-ttu-id="f25ce-122">Když je zobrazení vykresleno, v části se zobrazí v dolní části stránky HTML, klikněte pravým tlačítkem myši před uzavírací značku &lt;/body&gt; značky.</span><span class="sxs-lookup"><span data-stu-id="f25ce-122">When the view is rendered, the section appears at the bottom of the HTML page, right before the closing &lt;/body&gt; tag.</span></span>

<span data-ttu-id="f25ce-123">Všechny skriptu pro tuto stránku půjdou uvnitř značky script indikován komentář:</span><span class="sxs-lookup"><span data-stu-id="f25ce-123">All of the script for this page will go inside the script tag indicated by the comment:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample2.html)]

<span data-ttu-id="f25ce-124">Nejprve definujte třídu modelu zobrazení:</span><span class="sxs-lookup"><span data-stu-id="f25ce-124">First, define a view-model class:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample3.js)]

<span data-ttu-id="f25ce-125">**ko.observableArray** je zvláštní druh objektu v Knockout, volá se, *pozorovat*.</span><span class="sxs-lookup"><span data-stu-id="f25ce-125">**ko.observableArray** is a special kind of object in Knockout, called an *observable*.</span></span> <span data-ttu-id="f25ce-126">Z [dokumentaci rozhraní Knockout.js](http://knockoutjs.com/documentation/observables.html): Existuje zjištěný je "objekt jazyka JavaScript, který může upozornit předplatitele o změnách."</span><span class="sxs-lookup"><span data-stu-id="f25ce-126">From the [Knockout.js documentation](http://knockoutjs.com/documentation/observables.html): An observable is a "JavaScript object that can notify subscribers about changes."</span></span> <span data-ttu-id="f25ce-127">Při změně obsahu pozorovat, zobrazení se automaticky aktualizuje tak, aby odpovídaly.</span><span class="sxs-lookup"><span data-stu-id="f25ce-127">When the contents of an observable change, the view is automatically updated to match.</span></span>

<span data-ttu-id="f25ce-128">K naplnění `products` pole, zkontrolujte požadavek AJAX pro webové rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="f25ce-128">To populate the `products` array, make an AJAX request to the web API.</span></span> <span data-ttu-id="f25ce-129">Připomínáme, že jsme uložené základní identifikátor URI pro rozhraní API v kontejneru a zobrazení (viz [část 4](using-web-api-with-entity-framework-part-4.md) kurzu).</span><span class="sxs-lookup"><span data-stu-id="f25ce-129">Recall that we stored the base URI for the API in the view bag (see [Part 4](using-web-api-with-entity-framework-part-4.md) of the tutorial).</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample4.js?highlight=5)]

<span data-ttu-id="f25ce-130">Pak přidejte funkce do modelu zobrazení vytvářet, aktualizovat a odstraňovat produktů.</span><span class="sxs-lookup"><span data-stu-id="f25ce-130">Next, add functions to the view-model to create, update, and delete products.</span></span> <span data-ttu-id="f25ce-131">Tyto funkce odeslání volání AJAX pro webové rozhraní API a použijte k aktualizaci modelu zobrazení výsledků.</span><span class="sxs-lookup"><span data-stu-id="f25ce-131">These functions submit AJAX calls to the web API and use the results to update the view-model.</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample5.js?highlight=7)]

<span data-ttu-id="f25ce-132">Nyní nejdůležitější části: Při volání fulled načteno, modelu DOM **ko.applyBindings** fungovat a předejte mu novou instanci třídy `ProductsViewModel`:</span><span class="sxs-lookup"><span data-stu-id="f25ce-132">Now the most important part: When the DOM is fulled loaded, call the **ko.applyBindings** function and pass in a new instance of the `ProductsViewModel`:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample6.js)]

<span data-ttu-id="f25ce-133">**Ko.applyBindings** metoda aktivuje Knockout a sváže model zobrazení do zobrazení.</span><span class="sxs-lookup"><span data-stu-id="f25ce-133">The **ko.applyBindings** method activates Knockout and wires up the view-model to the view.</span></span>

<span data-ttu-id="f25ce-134">Když teď máme zobrazení modelu, můžeme vytvořit vazby.</span><span class="sxs-lookup"><span data-stu-id="f25ce-134">Now that we have a view-model, we can create the bindings.</span></span> <span data-ttu-id="f25ce-135">V rozhraní Knockout.js, můžete to provést přidáním `data-bind` atributy prvků HTML.</span><span class="sxs-lookup"><span data-stu-id="f25ce-135">In Knockout.js, you do this by adding `data-bind` attributes to HTML elements.</span></span> <span data-ttu-id="f25ce-136">Například pokud chcete svázat pole seznamu HTML, použijte `foreach` vazby:</span><span class="sxs-lookup"><span data-stu-id="f25ce-136">For example, to bind an HTML list to an array, use the `foreach` binding:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample7.html?highlight=1)]

<span data-ttu-id="f25ce-137">`foreach` Vazby Iteruje přes pole a vytvoří podřízené prvky pro každý objekt v poli.</span><span class="sxs-lookup"><span data-stu-id="f25ce-137">The `foreach` binding iterates through the array and creates child elements for each object in the array.</span></span> <span data-ttu-id="f25ce-138">Vazby na podřízené prvky mohou odkazovat na vlastnosti pole objektů.</span><span class="sxs-lookup"><span data-stu-id="f25ce-138">Bindings on the child elements can refer to properties on the array objects.</span></span>

<span data-ttu-id="f25ce-139">Přidejte následující vazby na seznam "aktualizace produktů":</span><span class="sxs-lookup"><span data-stu-id="f25ce-139">Add the following bindings to the "update-products" list:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample8.html)]

<span data-ttu-id="f25ce-140">`<li>` Element vyskytuje v rámci oboru **foreach** vazby.</span><span class="sxs-lookup"><span data-stu-id="f25ce-140">The `<li>` element occurs within the scope of the **foreach** binding.</span></span> <span data-ttu-id="f25ce-141">Že prostředky budou Knockout vykreslení elementu jednou pro každý produkt v `products` pole.</span><span class="sxs-lookup"><span data-stu-id="f25ce-141">That means Knockout will render the element once for each product in the `products` array.</span></span> <span data-ttu-id="f25ce-142">Všechny vazby v rámci `<li>` element odkazují na tuto instanci produktu.</span><span class="sxs-lookup"><span data-stu-id="f25ce-142">All of the bindings within the `<li>` element refer to that product instance.</span></span> <span data-ttu-id="f25ce-143">Například `$data.Name` odkazuje `Name` vlastnost na produktu.</span><span class="sxs-lookup"><span data-stu-id="f25ce-143">For example, `$data.Name` refers to the `Name` property on the product.</span></span>

<span data-ttu-id="f25ce-144">Pokud chcete nastavit hodnoty textovými vstupy, použijte `value` vazby.</span><span class="sxs-lookup"><span data-stu-id="f25ce-144">To set the values of the text inputs, use the `value` binding.</span></span> <span data-ttu-id="f25ce-145">Tlačítka jsou vázány na funkce na zobrazení modelu pomocí `click` vazby.</span><span class="sxs-lookup"><span data-stu-id="f25ce-145">The buttons are bound to functions on the model-view, using the `click` binding.</span></span> <span data-ttu-id="f25ce-146">Instance produktu je předán jako parametr pro každou funkci.</span><span class="sxs-lookup"><span data-stu-id="f25ce-146">The product instance is passed as a parameter to each function.</span></span> <span data-ttu-id="f25ce-147">Další informace najdete [dokumentaci rozhraní Knockout.js](http://knockoutjs.com/documentation/observables.html) má dobrý popis různých vazby.</span><span class="sxs-lookup"><span data-stu-id="f25ce-147">For more information, the [Knockout.js documentation](http://knockoutjs.com/documentation/observables.html) has good descriptions of the various bindings.</span></span>

<span data-ttu-id="f25ce-148">Dále přidejte vazbu pro **odeslat** událostí do formuláře přidat produktu:</span><span class="sxs-lookup"><span data-stu-id="f25ce-148">Next, add a binding for the **submit** event on the Add Product form:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample9.html)]

<span data-ttu-id="f25ce-149">Volá tuto vazbu `create` funkce na model zobrazení, chcete-li vytvořit nový produkt.</span><span class="sxs-lookup"><span data-stu-id="f25ce-149">This binding calls the `create` function on the view-model to create a new product.</span></span>

<span data-ttu-id="f25ce-150">Tady je kompletní kód pro zobrazení správce:</span><span class="sxs-lookup"><span data-stu-id="f25ce-150">Here is the complete code for the Admin view:</span></span>

[!code-cshtml[Main](using-web-api-with-entity-framework-part-5/samples/sample10.cshtml)]

<span data-ttu-id="f25ce-151">Spusťte aplikaci, přihlaste se pomocí účtu správce a klikněte na odkaz "Admin".</span><span class="sxs-lookup"><span data-stu-id="f25ce-151">Run the application, log in with the Administrator account, and click the "Admin" link.</span></span> <span data-ttu-id="f25ce-152">By měl zobrazit seznam produktů a být schopni vytvářet, aktualizovat nebo odstranit produktů.</span><span class="sxs-lookup"><span data-stu-id="f25ce-152">You should see the list of products, and be able to create, update, or delete products.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="f25ce-153">[Předchozí](using-web-api-with-entity-framework-part-4.md)
> [další](using-web-api-with-entity-framework-part-6.md)</span><span class="sxs-lookup"><span data-stu-id="f25ce-153">[Previous](using-web-api-with-entity-framework-part-4.md)
[Next](using-web-api-with-entity-framework-part-6.md)</span></span>
