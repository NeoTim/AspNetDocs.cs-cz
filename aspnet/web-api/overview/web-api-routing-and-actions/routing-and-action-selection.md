---
uid: web-api/overview/web-api-routing-and-actions/routing-and-action-selection
title: Směrování a výběr akcí ve webovém rozhraní API ASP.NET | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 12/14/2018
ms.assetid: bcf2d223-cb7f-411e-be05-f43e96a14015
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/routing-and-action-selection
msc.type: authoredcontent
ms.openlocfilehash: 62114e56fb29e80c93b82dcb78ce2bc2a123a83b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78554885"
---
# <a name="routing-and-action-selection-in-aspnet-web-api"></a><span data-ttu-id="3d6b6-102">Směrování a výběr akcí ve webovém rozhraní API ASP.NET</span><span class="sxs-lookup"><span data-stu-id="3d6b6-102">Routing and Action Selection in ASP.NET Web API</span></span>

<span data-ttu-id="3d6b6-103">o [Jan Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="3d6b6-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="3d6b6-104">Tento článek popisuje, jak webové rozhraní API ASP.NET směruje požadavek HTTP na určitou akci na řadiči.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-104">This article describes how ASP.NET Web API routes an HTTP request to a particular action on a controller.</span></span>

> [!NOTE]
> <span data-ttu-id="3d6b6-105">Podrobný přehled směrování najdete v tématu [směrování ve webovém rozhraní API ASP.NET](routing-in-aspnet-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="3d6b6-105">For a high-level overview of routing, see [Routing in ASP.NET Web API](routing-in-aspnet-web-api.md).</span></span>

<span data-ttu-id="3d6b6-106">V tomto článku se podíváme na podrobnosti o procesu směrování.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-106">This article looks at the details of the routing process.</span></span> <span data-ttu-id="3d6b6-107">Pokud vytvoříte projekt webového rozhraní API a zjistíte, že některé požadavky nejsou směrovány očekávaným způsobem, snad tohoto článku vám pomůže.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-107">If you create a Web API project and find that some requests don't get routed the way you expect, hopefully this article will help.</span></span>

<span data-ttu-id="3d6b6-108">Směrování má tři hlavní fáze:</span><span class="sxs-lookup"><span data-stu-id="3d6b6-108">Routing has three main phases:</span></span>

1. <span data-ttu-id="3d6b6-109">Identifikátor URI se shoduje s šablonou trasy.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-109">Matching the URI to a route template.</span></span>
2. <span data-ttu-id="3d6b6-110">Výběr kontroleru.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-110">Selecting a controller.</span></span>
3. <span data-ttu-id="3d6b6-111">Výběr akce</span><span class="sxs-lookup"><span data-stu-id="3d6b6-111">Selecting an action.</span></span>

<span data-ttu-id="3d6b6-112">Některé části procesu můžete nahradit vlastními chováními.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-112">You can replace some parts of the process with your own custom behaviors.</span></span> <span data-ttu-id="3d6b6-113">V tomto článku jsme popsali výchozí chování.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-113">In this article, I describe the default behavior.</span></span> <span data-ttu-id="3d6b6-114">Na konci se označují místa, kde můžete přizpůsobit chování.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-114">At the end, I note the places where you can customize the behavior.</span></span>

## <a name="route-templates"></a><span data-ttu-id="3d6b6-115">Šablony směrování</span><span class="sxs-lookup"><span data-stu-id="3d6b6-115">Route Templates</span></span>

<span data-ttu-id="3d6b6-116">Šablona trasy vypadá podobně jako cesta URI, ale může mít zástupné hodnoty označené složenými závorkami:</span><span class="sxs-lookup"><span data-stu-id="3d6b6-116">A route template looks similar to a URI path, but it can have placeholder values, indicated with curly braces:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample1.ps1)]

<span data-ttu-id="3d6b6-117">Při vytváření trasy můžete zadat výchozí hodnoty pro některé nebo všechny zástupné symboly:</span><span class="sxs-lookup"><span data-stu-id="3d6b6-117">When you create a route, you can provide default values for some or all of the placeholders:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample2.cs)]

<span data-ttu-id="3d6b6-118">Můžete také poskytnout omezení, která omezují, jak může segment URI odpovídat zástupnému symbolu:</span><span class="sxs-lookup"><span data-stu-id="3d6b6-118">You can also provide constraints, which restrict how a URI segment can match a placeholder:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample3.js)]

<span data-ttu-id="3d6b6-119">Rozhraní se pokusí vyhledat segmenty v cestě identifikátoru URI k šabloně.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-119">The framework tries to match the segments in the URI path to the template.</span></span> <span data-ttu-id="3d6b6-120">Literály v šabloně se musí přesně shodovat.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-120">Literals in the template must match exactly.</span></span> <span data-ttu-id="3d6b6-121">Zástupný text odpovídá jakékoli hodnotě, pokud nezadáte omezení.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-121">A placeholder matches any value, unless you specify constraints.</span></span> <span data-ttu-id="3d6b6-122">Rozhraní se neshoduje s ostatními částmi identifikátoru URI, jako je název hostitele nebo parametry dotazu.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-122">The framework does not match other parts of the URI, such as the host name or the query parameters.</span></span> <span data-ttu-id="3d6b6-123">Rozhraní vybere první trasu v tabulce směrování, která odpovídá identifikátoru URI.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-123">The framework selects the first route in the route table that matches the URI.</span></span>

<span data-ttu-id="3d6b6-124">Existují dva speciální zástupné symboly: {Controller} a {Action}.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-124">There are two special placeholders: "{controller}" and "{action}".</span></span>

- <span data-ttu-id="3d6b6-125">{Controller} poskytuje název kontroleru.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-125">"{controller}" provides the name of the controller.</span></span>
- <span data-ttu-id="3d6b6-126">"{Action}" poskytuje název akce.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-126">"{action}" provides the name of the action.</span></span> <span data-ttu-id="3d6b6-127">V rámci webového rozhraní API je obvyklá konvence vynechat {Action}.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-127">In Web API, the usual convention is to omit "{action}".</span></span>

### <a name="defaults"></a><span data-ttu-id="3d6b6-128">Ve výchozím nastavení</span><span class="sxs-lookup"><span data-stu-id="3d6b6-128">Defaults</span></span>

<span data-ttu-id="3d6b6-129">Pokud zadáte výchozí hodnoty, bude trasa odpovídat identifikátoru URI, u kterého tyto segmenty chybí.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-129">If you provide defaults, the route will match a URI that is missing those segments.</span></span> <span data-ttu-id="3d6b6-130">Příklad:</span><span class="sxs-lookup"><span data-stu-id="3d6b6-130">For example:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample4.cs)]

<span data-ttu-id="3d6b6-131">Identifikátory URI `http://localhost/api/products/all` a `http://localhost/api/products` odpovídají předchozí trase.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-131">The URIs `http://localhost/api/products/all` and `http://localhost/api/products` match the preceding route.</span></span> <span data-ttu-id="3d6b6-132">V druhém identifikátoru URI má `{category}` k chybějícímu segmentu přiřazenou výchozí hodnotu `all`.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-132">In the latter URI, the missing `{category}` segment is assigned the default value `all`.</span></span>

### <a name="route-dictionary"></a><span data-ttu-id="3d6b6-133">Slovník směrování</span><span class="sxs-lookup"><span data-stu-id="3d6b6-133">Route Dictionary</span></span>

<span data-ttu-id="3d6b6-134">Pokud rozhraní nalezne shodu pro identifikátor URI, vytvoří slovník, který obsahuje hodnotu pro každý zástupný text.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-134">If the framework finds a match for a URI, it creates a dictionary that contains the value for each placeholder.</span></span> <span data-ttu-id="3d6b6-135">Klíče jsou zástupné názvy, včetně složených závorek.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-135">The keys are the placeholder names, not including the curly braces.</span></span> <span data-ttu-id="3d6b6-136">Hodnoty jsou přijímány z cesty identifikátoru URI nebo z výchozího nastavení.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-136">The values are taken from the URI path or from the defaults.</span></span> <span data-ttu-id="3d6b6-137">Slovník je uložen v objektu **IHttpRouteData** .</span><span class="sxs-lookup"><span data-stu-id="3d6b6-137">The dictionary is stored in the **IHttpRouteData** object.</span></span>

<span data-ttu-id="3d6b6-138">Během této fáze pro porovnání tras se speciální zástupné symboly {Controller} a {Action} považují za stejné jako jiné zástupné symboly.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-138">During this route-matching phase, the special "{controller}" and "{action}" placeholders are treated just like the other placeholders.</span></span> <span data-ttu-id="3d6b6-139">Jsou jednoduše uloženy ve slovníku s ostatními hodnotami.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-139">They are simply stored in the dictionary with the other values.</span></span>

<span data-ttu-id="3d6b6-140">Výchozí hodnota může mít speciální hodnotu **RouteParameter. volitelné**.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-140">A default can have the special value **RouteParameter.Optional**.</span></span> <span data-ttu-id="3d6b6-141">Pokud se této hodnotě přiřadí zástupný text, hodnota se nepřidá do slovníku směrování.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-141">If a placeholder gets assigned this value, the value is not added to the route dictionary.</span></span> <span data-ttu-id="3d6b6-142">Příklad:</span><span class="sxs-lookup"><span data-stu-id="3d6b6-142">For example:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample5.cs)]

<span data-ttu-id="3d6b6-143">Pro cestu identifikátoru URI "API/Products" bude mít slovník tras:</span><span class="sxs-lookup"><span data-stu-id="3d6b6-143">For the URI path "api/products", the route dictionary will contain:</span></span>

- <span data-ttu-id="3d6b6-144">kontroler: "Products"</span><span class="sxs-lookup"><span data-stu-id="3d6b6-144">controller: "products"</span></span>
- <span data-ttu-id="3d6b6-145">Kategorie: vše</span><span class="sxs-lookup"><span data-stu-id="3d6b6-145">category: "all"</span></span>

<span data-ttu-id="3d6b6-146">Pro "API/Products/Toys/123" ale bude mít tento slovník tras:</span><span class="sxs-lookup"><span data-stu-id="3d6b6-146">For "api/products/toys/123", however, the route dictionary will contain:</span></span>

- <span data-ttu-id="3d6b6-147">kontroler: "Products"</span><span class="sxs-lookup"><span data-stu-id="3d6b6-147">controller: "products"</span></span>
- <span data-ttu-id="3d6b6-148">Kategorie: "hračky"</span><span class="sxs-lookup"><span data-stu-id="3d6b6-148">category: "toys"</span></span>
- <span data-ttu-id="3d6b6-149">ID: "123"</span><span class="sxs-lookup"><span data-stu-id="3d6b6-149">id: "123"</span></span>

<span data-ttu-id="3d6b6-150">Výchozí hodnoty mohou také obsahovat hodnotu, která se nezobrazí kdekoli v šabloně trasy.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-150">The defaults can also include a value that does not appear anywhere in the route template.</span></span> <span data-ttu-id="3d6b6-151">Pokud trasa odpovídá, je tato hodnota uložena ve slovníku.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-151">If the route matches, that value is stored in the dictionary.</span></span> <span data-ttu-id="3d6b6-152">Příklad:</span><span class="sxs-lookup"><span data-stu-id="3d6b6-152">For example:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample6.cs)]

<span data-ttu-id="3d6b6-153">Pokud je cesta URI "API/root/8", bude mít slovník dvě hodnoty:</span><span class="sxs-lookup"><span data-stu-id="3d6b6-153">If the URI path is "api/root/8", the dictionary will contain two values:</span></span>

- <span data-ttu-id="3d6b6-154">kontroler: "Customers"</span><span class="sxs-lookup"><span data-stu-id="3d6b6-154">controller: "customers"</span></span>
- <span data-ttu-id="3d6b6-155">ID: "8"</span><span class="sxs-lookup"><span data-stu-id="3d6b6-155">id: "8"</span></span>

## <a name="selecting-a-controller"></a><span data-ttu-id="3d6b6-156">Výběr kontroleru</span><span class="sxs-lookup"><span data-stu-id="3d6b6-156">Selecting a Controller</span></span>

<span data-ttu-id="3d6b6-157">Výběr kontroleru se zpracovává metodou **IHttpControllerSelector. SelectController** .</span><span class="sxs-lookup"><span data-stu-id="3d6b6-157">Controller selection is handled by the **IHttpControllerSelector.SelectController** method.</span></span> <span data-ttu-id="3d6b6-158">Tato metoda přebírá instanci **zprávy HttpRequestMessage** a vrací **HttpControllerDescriptor**.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-158">This method takes an **HttpRequestMessage** instance and returns an **HttpControllerDescriptor**.</span></span> <span data-ttu-id="3d6b6-159">Výchozí implementace je poskytována třídou **DefaultHttpControllerSelector** .</span><span class="sxs-lookup"><span data-stu-id="3d6b6-159">The default implementation is provided by the **DefaultHttpControllerSelector** class.</span></span> <span data-ttu-id="3d6b6-160">Tato třída používá přímočarý algoritmus:</span><span class="sxs-lookup"><span data-stu-id="3d6b6-160">This class uses a straightforward algorithm:</span></span>

1. <span data-ttu-id="3d6b6-161">Podívejte se do slovníku tras pro klíč "Controller".</span><span class="sxs-lookup"><span data-stu-id="3d6b6-161">Look in the route dictionary for the key "controller".</span></span>
2. <span data-ttu-id="3d6b6-162">Pokud chcete získat název typu kontroléru, přečtěte si hodnotu tohoto klíče a přidejte do něj řetězec "Controller".</span><span class="sxs-lookup"><span data-stu-id="3d6b6-162">Take the value for this key and append the string "Controller" to get the controller type name.</span></span>
3. <span data-ttu-id="3d6b6-163">Vyhledejte kontroler webového rozhraní API s tímto názvem typu.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-163">Look for a Web API controller with this type name.</span></span>

<span data-ttu-id="3d6b6-164">Pokud například adresář tras obsahuje dvojici klíč-hodnota "Controller" = "Products", pak je typ kontroleru "ProductsController".</span><span class="sxs-lookup"><span data-stu-id="3d6b6-164">For example, if the route dictionary contains the key-value pair "controller" = "products", then the controller type is "ProductsController".</span></span> <span data-ttu-id="3d6b6-165">Pokud neexistuje odpovídající typ ani více shod, rozhraní vrátí chybu klientovi.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-165">If there is no matching type, or multiple matches, the framework returns an error to the client.</span></span>

<span data-ttu-id="3d6b6-166">V kroku 3 **DefaultHttpControllerSelector** používá rozhraní **IHttpControllerTypeResolver** k získání seznamu typů řadičů webového rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-166">For step 3, **DefaultHttpControllerSelector** uses the **IHttpControllerTypeResolver** interface to get the list of Web API controller types.</span></span> <span data-ttu-id="3d6b6-167">Výchozí implementace **IHttpControllerTypeResolver** vrátí všechny veřejné třídy, které (a) implementují **IHttpController**, (b) nejsou abstraktní a (c) mají název, který končí na "Controller".</span><span class="sxs-lookup"><span data-stu-id="3d6b6-167">The default implementation of **IHttpControllerTypeResolver** returns all public classes that (a) implement **IHttpController**, (b) are not abstract, and (c) have a name that ends in "Controller".</span></span>

## <a name="action-selection"></a><span data-ttu-id="3d6b6-168">Výběr akce</span><span class="sxs-lookup"><span data-stu-id="3d6b6-168">Action Selection</span></span>

<span data-ttu-id="3d6b6-169">Po výběru kontroleru vybere architektura akci voláním metody **IHttpActionSelector. SelectAction** .</span><span class="sxs-lookup"><span data-stu-id="3d6b6-169">After selecting the controller, the framework selects the action by calling the **IHttpActionSelector.SelectAction** method.</span></span> <span data-ttu-id="3d6b6-170">Tato metoda přijímá **HttpControllerContext** a vrací **HttpActionDescriptor**.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-170">This method takes an **HttpControllerContext** and returns an **HttpActionDescriptor**.</span></span>

<span data-ttu-id="3d6b6-171">Výchozí implementace je poskytována třídou **ApiControllerActionSelector** .</span><span class="sxs-lookup"><span data-stu-id="3d6b6-171">The default implementation is provided by the **ApiControllerActionSelector** class.</span></span> <span data-ttu-id="3d6b6-172">Pokud chcete vybrat akci, podívejte se na následující:</span><span class="sxs-lookup"><span data-stu-id="3d6b6-172">To select an action, it looks at the following:</span></span>

- <span data-ttu-id="3d6b6-173">Metoda HTTP požadavku.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-173">The HTTP method of the request.</span></span>
- <span data-ttu-id="3d6b6-174">Zástupný symbol {Action} v šabloně směrování, pokud je k dispozici.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-174">The "{action}" placeholder in the route template, if present.</span></span>
- <span data-ttu-id="3d6b6-175">Parametry akcí na řadiči.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-175">The parameters of the actions on the controller.</span></span>

<span data-ttu-id="3d6b6-176">Než začnete s algoritmem výběru, musíme pochopit některé věci o akcích kontroleru.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-176">Before looking at the selection algorithm, we need to understand some things about controller actions.</span></span>

<span data-ttu-id="3d6b6-177">**Které metody kontroleru se považují za "akce"?**</span><span class="sxs-lookup"><span data-stu-id="3d6b6-177">**Which methods on the controller are considered "actions"?**</span></span> <span data-ttu-id="3d6b6-178">Při výběru akce rozhraní vyhledá pouze veřejné metody instance v řadiči.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-178">When selecting an action, the framework only looks at public instance methods on the controller.</span></span> <span data-ttu-id="3d6b6-179">Kromě toho vylučuje metody ["speciálního názvu"](https://msdn.microsoft.com/library/system.reflection.methodbase.isspecialname) (konstruktory, události, přetížení operátoru a tak dále) a metody zděděné z třídy **ApiController** .</span><span class="sxs-lookup"><span data-stu-id="3d6b6-179">Also, it excludes ["special name"](https://msdn.microsoft.com/library/system.reflection.methodbase.isspecialname) methods (constructors, events, operator overloads, and so forth), and methods inherited from the **ApiController** class.</span></span>

<span data-ttu-id="3d6b6-180">**Metody HTTP.**</span><span class="sxs-lookup"><span data-stu-id="3d6b6-180">**HTTP Methods.**</span></span> <span data-ttu-id="3d6b6-181">Rozhraní vybere pouze akce, které odpovídají metodě HTTP žádosti, určené následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="3d6b6-181">The framework only chooses actions that match the HTTP method of the request, determined as follows:</span></span>

1. <span data-ttu-id="3d6b6-182">Metodu HTTP můžete zadat s atributem: **AcceptVerbs**, **HttpDelete**, **HttpGet**, **HttpHead**, **HttpOptions**, **HttpPatch**, **HTTPPOST**nebo **HttpPut**.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-182">You can specify the HTTP method with an attribute: **AcceptVerbs**, **HttpDelete**, **HttpGet**, **HttpHead**, **HttpOptions**, **HttpPatch**, **HttpPost**, or **HttpPut**.</span></span>
2. <span data-ttu-id="3d6b6-183">V opačném případě, pokud název metody kontroleru začíná na "Get", "post", "Put", "Delete", "Head", "Options" nebo "patch", pak podle konvence akce podporuje tuto metodu HTTP.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-183">Otherwise, if the name of the controller method starts with "Get", "Post", "Put", "Delete", "Head", "Options", or "Patch", then by convention the action supports that HTTP method.</span></span>
3. <span data-ttu-id="3d6b6-184">Pokud žádný z výše uvedeného není, metoda podporuje POST.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-184">If none of the above, the method supports POST.</span></span>

<span data-ttu-id="3d6b6-185">**Vazby parametrů**</span><span class="sxs-lookup"><span data-stu-id="3d6b6-185">**Parameter Bindings.**</span></span> <span data-ttu-id="3d6b6-186">Vazba parametru je způsob, jakým webové rozhraní API vytvoří hodnotu pro parametr.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-186">A parameter binding is how Web API creates a value for a parameter.</span></span> <span data-ttu-id="3d6b6-187">Toto je výchozí pravidlo pro vazbu parametru:</span><span class="sxs-lookup"><span data-stu-id="3d6b6-187">Here is the default rule for parameter binding:</span></span>

- <span data-ttu-id="3d6b6-188">Z identifikátoru URI jsou přijímány jednoduché typy.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-188">Simple types are taken from the URI.</span></span>
- <span data-ttu-id="3d6b6-189">Komplexní typy jsou odebírány z textu žádosti.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-189">Complex types are taken from the request body.</span></span>

<span data-ttu-id="3d6b6-190">Jednoduché typy zahrnují všechny [.NET Framework primitivních typů](https://msdn.microsoft.com/library/system.type.isprimitive)plus **DateTime**, **Decimal**, **GUID**, **String**a **TimeSpan**.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-190">Simple types include all of the [.NET Framework primitive types](https://msdn.microsoft.com/library/system.type.isprimitive), plus **DateTime**, **Decimal**, **Guid**, **String**, and **TimeSpan**.</span></span> <span data-ttu-id="3d6b6-191">Pro každou akci může tělo žádosti přečíst maximálně jeden parametr.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-191">For each action, at most one parameter can read the request body.</span></span>

> [!NOTE]
> <span data-ttu-id="3d6b6-192">Je možné přepsat výchozí pravidla vazby.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-192">It is possible to override the default binding rules.</span></span> <span data-ttu-id="3d6b6-193">Viz [vazba parametrů WebApi v digestoři](https://blogs.msdn.com/b/jmstall/archive/2012/05/11/webapi-parameter-binding-under-the-hood.aspx).</span><span class="sxs-lookup"><span data-stu-id="3d6b6-193">See [WebAPI Parameter binding under the hood](https://blogs.msdn.com/b/jmstall/archive/2012/05/11/webapi-parameter-binding-under-the-hood.aspx).</span></span>

<span data-ttu-id="3d6b6-194">S tímto pozadím je tady algoritmus výběru akce.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-194">With that background, here is the action selection algorithm.</span></span>

1. <span data-ttu-id="3d6b6-195">Vytvoří seznam všech akcí na řadiči, které odpovídají metodě požadavku HTTP.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-195">Create a list of all actions on the controller that match the HTTP request method.</span></span>
2. <span data-ttu-id="3d6b6-196">Pokud má slovník tras položku "Action" (akce), odeberte akce, jejichž název neodpovídá této hodnotě.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-196">If the route dictionary has an "action" entry, remove actions whose name does not match this value.</span></span>
3. <span data-ttu-id="3d6b6-197">Zkuste porovnat parametry akce s identifikátorem URI následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="3d6b6-197">Try to match action parameters to the URI, as follows:</span></span> 

    1. <span data-ttu-id="3d6b6-198">Pro každou akci Získejte seznam parametrů, které jsou jednoduchého typu, kde vazba získá parametr z identifikátoru URI.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-198">For each action, get a list of the parameters that are a simple type, where the binding gets the parameter from the URI.</span></span> <span data-ttu-id="3d6b6-199">Vylučte volitelné parametry.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-199">Exclude optional parameters.</span></span>
    2. <span data-ttu-id="3d6b6-200">V tomto seznamu zkuste najít shodu pro každý název parametru, a to buď ve slovníku směrování, nebo v řetězci dotazu URI.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-200">From this list, try to find a match for each parameter name, either in the route dictionary or in the URI query string.</span></span> <span data-ttu-id="3d6b6-201">Shoda rozlišuje velká a malá písmena a nezávisí na pořadí parametrů.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-201">Matches are case insensitive and do not depend on the parameter order.</span></span>
    3. <span data-ttu-id="3d6b6-202">Vyberte akci, u které má každý parametr v seznamu shodu s identifikátorem URI.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-202">Select an action where every parameter in the list has a match in the URI.</span></span>
    4. <span data-ttu-id="3d6b6-203">Pokud tato kritéria splňují více než jedna akce, vyberte ji s nejvíce shodami parametrů.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-203">If more that one action meets these criteria, pick the one with the most parameter matches.</span></span>
4. <span data-ttu-id="3d6b6-204">Ignoruje akce s atributem **[neaction]** .</span><span class="sxs-lookup"><span data-stu-id="3d6b6-204">Ignore actions with the **[NonAction]** attribute.</span></span>

<span data-ttu-id="3d6b6-205">Krok #3 je pravděpodobně nejvíce matoucí.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-205">Step #3 is probably the most confusing.</span></span> <span data-ttu-id="3d6b6-206">Základní nápad je, že parametr může získat svou hodnotu buď z identifikátoru URI, z textu žádosti, nebo z vlastní vazby.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-206">The basic idea is that a parameter can get its value either from the URI, from the request body, or from a custom binding.</span></span> <span data-ttu-id="3d6b6-207">Pro parametry, které pocházejí z identifikátoru URI, chceme zajistit, aby identifikátor URI ve skutečnosti obsahoval hodnotu pro tento parametr, buď v cestě (prostřednictvím slovníku směrování), nebo v řetězci dotazu.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-207">For parameters that come from the URI, we want to ensure that the URI actually contains a value for that parameter, either in the path (via the route dictionary) or in the query string.</span></span>

<span data-ttu-id="3d6b6-208">Zvažte například následující akci:</span><span class="sxs-lookup"><span data-stu-id="3d6b6-208">For example, consider the following action:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample7.cs)]

<span data-ttu-id="3d6b6-209">Parametr *ID* se váže k identifikátoru URI.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-209">The *id* parameter binds to the URI.</span></span> <span data-ttu-id="3d6b6-210">Proto se tato akce může shodovat jenom s identifikátorem URI, který obsahuje hodnotu pro "ID", a to buď ve slovníku směrování, nebo v řetězci dotazu.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-210">Therefore, this action can only match a URI that contains a value for "id", either in the route dictionary or in the query string.</span></span>

<span data-ttu-id="3d6b6-211">Volitelné parametry jsou výjimkou, protože jsou nepovinné.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-211">Optional parameters are an exception, because they are optional.</span></span> <span data-ttu-id="3d6b6-212">U volitelného parametru je to v pořádku, pokud vazba nemůže získat hodnotu z identifikátoru URI.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-212">For an optional parameter, it's OK if the binding can't get the value from the URI.</span></span>

<span data-ttu-id="3d6b6-213">Komplexní typy jsou výjimkou z jiného důvodu.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-213">Complex types are an exception for a different reason.</span></span> <span data-ttu-id="3d6b6-214">Komplexní typ se dá svázat jenom s identifikátorem URI prostřednictvím vlastní vazby.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-214">A complex type can only bind to the URI through a custom binding.</span></span> <span data-ttu-id="3d6b6-215">V takovém případě ale rozhraní nemůže bez ohledu na to, jestli parametr vytvoří vazby na konkrétní identifikátor URI.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-215">But in that case, the framework cannot know in advance whether the parameter would bind to a particular URI.</span></span> <span data-ttu-id="3d6b6-216">Aby bylo možné zjistit, bude nutné vyvolat vazbu.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-216">To find out, it would need to invoke the binding.</span></span> <span data-ttu-id="3d6b6-217">Cílem algoritmu výběru je vybrat akci ze statického popisu před vyvoláním jakýchkoli vazeb.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-217">The goal of the selection algorithm is to select an action from the static description, before invoking any bindings.</span></span> <span data-ttu-id="3d6b6-218">Proto jsou komplexní typy vyloučeny z odpovídajícího algoritmu.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-218">Therefore, complex types are excluded from the matching algorithm.</span></span>

<span data-ttu-id="3d6b6-219">Po výběru akce jsou vyvolány všechny vazby parametrů.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-219">After the action is selected, all parameter bindings are invoked.</span></span>

<span data-ttu-id="3d6b6-220">Souhrn:</span><span class="sxs-lookup"><span data-stu-id="3d6b6-220">Summary:</span></span>

- <span data-ttu-id="3d6b6-221">Akce musí odpovídat metodě HTTP žádosti.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-221">The action must match the HTTP method of the request.</span></span>
- <span data-ttu-id="3d6b6-222">Název akce se musí shodovat s položkou "Action" ve slovníku směrování, pokud je k dispozici.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-222">The action name must match the "action" entry in the route dictionary, if present.</span></span>
- <span data-ttu-id="3d6b6-223">U každého parametru akce, pokud je parametr z identifikátoru URI, musí být název parametru nalezen buď ve slovníku směrování, nebo v řetězci dotazu identifikátoru URI.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-223">For every parameter of the action, if the parameter is taken from the URI, then the parameter name must be found either in the route dictionary or in the URI query string.</span></span> <span data-ttu-id="3d6b6-224">(Volitelné parametry a parametry se složitými typy jsou vyloučeny.)</span><span class="sxs-lookup"><span data-stu-id="3d6b6-224">(Optional parameters and parameters with complex types are excluded.)</span></span>
- <span data-ttu-id="3d6b6-225">Snažte se porovnat s největším počtem parametrů.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-225">Try to match the most number of parameters.</span></span> <span data-ttu-id="3d6b6-226">Nejlepší shoda může být metoda bez parametrů.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-226">The best match might be a method with no parameters.</span></span>

## <a name="extended-example"></a><span data-ttu-id="3d6b6-227">Rozšířený příklad</span><span class="sxs-lookup"><span data-stu-id="3d6b6-227">Extended Example</span></span>

<span data-ttu-id="3d6b6-228">Tras</span><span class="sxs-lookup"><span data-stu-id="3d6b6-228">Routes:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample8.cs)]

<span data-ttu-id="3d6b6-229">Kontroler:</span><span class="sxs-lookup"><span data-stu-id="3d6b6-229">Controller:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample9.cs)]

<span data-ttu-id="3d6b6-230">Požadavek HTTP:</span><span class="sxs-lookup"><span data-stu-id="3d6b6-230">HTTP request:</span></span>

[!code-console[Main](routing-and-action-selection/samples/sample10.cmd)]

### <a name="route-matching"></a><span data-ttu-id="3d6b6-231">Shoda trasy</span><span class="sxs-lookup"><span data-stu-id="3d6b6-231">Route Matching</span></span>

<span data-ttu-id="3d6b6-232">Identifikátor URI odpovídá trase s názvem "DefaultApi".</span><span class="sxs-lookup"><span data-stu-id="3d6b6-232">The URI matches the route named "DefaultApi".</span></span> <span data-ttu-id="3d6b6-233">Slovník tras obsahuje následující položky:</span><span class="sxs-lookup"><span data-stu-id="3d6b6-233">The route dictionary contains the following entries:</span></span>

- <span data-ttu-id="3d6b6-234">kontroler: "Products"</span><span class="sxs-lookup"><span data-stu-id="3d6b6-234">controller: "products"</span></span>
- <span data-ttu-id="3d6b6-235">ID: "1"</span><span class="sxs-lookup"><span data-stu-id="3d6b6-235">id: "1"</span></span>

<span data-ttu-id="3d6b6-236">Slovník tras neobsahuje parametry řetězce dotazu, "Version" a "Details", ale ty se budou i nadále brát v potaz během výběru akce.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-236">The route dictionary does not contain the query string parameters, "version" and "details", but these will still be considered during action selection.</span></span>

### <a name="controller-selection"></a><span data-ttu-id="3d6b6-237">Výběr kontroleru</span><span class="sxs-lookup"><span data-stu-id="3d6b6-237">Controller Selection</span></span>

<span data-ttu-id="3d6b6-238">Z položky "Controller" v adresáři směrování je typ kontroleru `ProductsController`.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-238">From the "controller" entry in the route dictionary, the controller type is `ProductsController`.</span></span>

### <a name="action-selection"></a><span data-ttu-id="3d6b6-239">Výběr akce</span><span class="sxs-lookup"><span data-stu-id="3d6b6-239">Action Selection</span></span>

<span data-ttu-id="3d6b6-240">Požadavek HTTP je požadavek GET.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-240">The HTTP request is a GET request.</span></span> <span data-ttu-id="3d6b6-241">Akce kontroleru, které podporují GET, jsou `GetAll`, `GetById`a `FindProductsByName`.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-241">The controller actions that support GET are `GetAll`, `GetById`, and `FindProductsByName`.</span></span> <span data-ttu-id="3d6b6-242">Slovník tras neobsahuje položku "Action", takže nemusíme odpovídat názvu akce.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-242">The route dictionary does not contain an entry for "action", so we don't need to match the action name.</span></span>

<span data-ttu-id="3d6b6-243">V dalším kroku se podíváme na názvy parametrů pro akce, a to jenom v akci GET.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-243">Next, we try to match parameter names for the actions, looking only at the GET actions.</span></span>

| <span data-ttu-id="3d6b6-244">Akce</span><span class="sxs-lookup"><span data-stu-id="3d6b6-244">Action</span></span> | <span data-ttu-id="3d6b6-245">Parametry, které se mají spárovat</span><span class="sxs-lookup"><span data-stu-id="3d6b6-245">Parameters to Match</span></span> |
| --- | --- |
| `GetAll` | <span data-ttu-id="3d6b6-246">Žádná</span><span class="sxs-lookup"><span data-stu-id="3d6b6-246">none</span></span> |
| `GetById` | <span data-ttu-id="3d6b6-247">účet</span><span class="sxs-lookup"><span data-stu-id="3d6b6-247">"id"</span></span> |
| `FindProductsByName` | <span data-ttu-id="3d6b6-248">název</span><span class="sxs-lookup"><span data-stu-id="3d6b6-248">"name"</span></span> |

<span data-ttu-id="3d6b6-249">Všimněte si, že parametr *verze* `GetById` není považován za, protože se jedná o volitelný parametr.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-249">Notice that the *version* parameter of `GetById` is not considered, because it is an optional parameter.</span></span>

<span data-ttu-id="3d6b6-250">Metoda `GetAll` odpovídá triviálnímu.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-250">The `GetAll` method matches trivially.</span></span> <span data-ttu-id="3d6b6-251">Metoda `GetById` také odpovídá, protože slovník směrování obsahuje "ID".</span><span class="sxs-lookup"><span data-stu-id="3d6b6-251">The `GetById` method also matches, because the route dictionary contains "id".</span></span> <span data-ttu-id="3d6b6-252">Metoda `FindProductsByName` se neshoduje.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-252">The `FindProductsByName` method does not match.</span></span>

<span data-ttu-id="3d6b6-253">Služba `GetById` metoda WINS, protože se shoduje s jedním parametrem, bez parametrů pro `GetAll`.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-253">The `GetById` method wins, because it matches one parameter, versus no parameters for `GetAll`.</span></span> <span data-ttu-id="3d6b6-254">Metoda je vyvolána s následujícími hodnotami parametrů:</span><span class="sxs-lookup"><span data-stu-id="3d6b6-254">The method is invoked with the following parameter values:</span></span>

- <span data-ttu-id="3d6b6-255">*ID* = 1</span><span class="sxs-lookup"><span data-stu-id="3d6b6-255">*id* = 1</span></span>
- <span data-ttu-id="3d6b6-256">*verze* = 1,5</span><span class="sxs-lookup"><span data-stu-id="3d6b6-256">*version* = 1.5</span></span>

<span data-ttu-id="3d6b6-257">Všimněte si, že i když se *verze* v algoritmu výběru nepoužila, hodnota parametru přichází z řetězce dotazu identifikátoru URI.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-257">Notice that even though *version* was not used in the selection algorithm, the value of the parameter comes from the URI query string.</span></span>

## <a name="extension-points"></a><span data-ttu-id="3d6b6-258">Rozšiřovací body</span><span class="sxs-lookup"><span data-stu-id="3d6b6-258">Extension Points</span></span>

<span data-ttu-id="3d6b6-259">Webové rozhraní API poskytuje body rozšíření pro některé části procesu směrování.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-259">Web API provides extension points for some parts of the routing process.</span></span>

| <span data-ttu-id="3d6b6-260">Rozhraní</span><span class="sxs-lookup"><span data-stu-id="3d6b6-260">Interface</span></span> | <span data-ttu-id="3d6b6-261">Popis</span><span class="sxs-lookup"><span data-stu-id="3d6b6-261">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3d6b6-262">**IHttpControllerSelector**</span><span class="sxs-lookup"><span data-stu-id="3d6b6-262">**IHttpControllerSelector**</span></span> | <span data-ttu-id="3d6b6-263">Vybere kontroler.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-263">Selects the controller.</span></span> |
| <span data-ttu-id="3d6b6-264">**IHttpControllerTypeResolver**</span><span class="sxs-lookup"><span data-stu-id="3d6b6-264">**IHttpControllerTypeResolver**</span></span> | <span data-ttu-id="3d6b6-265">Získá seznam typů kontroléru.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-265">Gets the list of controller types.</span></span> <span data-ttu-id="3d6b6-266">**DefaultHttpControllerSelector** zvolí typ kontroleru z tohoto seznamu.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-266">The **DefaultHttpControllerSelector** chooses the controller type from this list.</span></span> |
| <span data-ttu-id="3d6b6-267">**IAssembliesResolver**</span><span class="sxs-lookup"><span data-stu-id="3d6b6-267">**IAssembliesResolver**</span></span> | <span data-ttu-id="3d6b6-268">Získá seznam sestavení projektu.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-268">Gets the list of project assemblies.</span></span> <span data-ttu-id="3d6b6-269">Rozhraní **IHttpControllerTypeResolver** používá tento seznam k nalezení typů kontroleru.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-269">The **IHttpControllerTypeResolver** interface uses this list to find the controller types.</span></span> |
| <span data-ttu-id="3d6b6-270">**IHttpControllerActivator**</span><span class="sxs-lookup"><span data-stu-id="3d6b6-270">**IHttpControllerActivator**</span></span> | <span data-ttu-id="3d6b6-271">Vytvoří nové instance kontroleru.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-271">Creates new controller instances.</span></span> |
| <span data-ttu-id="3d6b6-272">**IHttpActionSelector**</span><span class="sxs-lookup"><span data-stu-id="3d6b6-272">**IHttpActionSelector**</span></span> | <span data-ttu-id="3d6b6-273">Vybere akci.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-273">Selects the action.</span></span> |
| <span data-ttu-id="3d6b6-274">**IHttpActionInvoker**</span><span class="sxs-lookup"><span data-stu-id="3d6b6-274">**IHttpActionInvoker**</span></span> | <span data-ttu-id="3d6b6-275">Vyvolá akci.</span><span class="sxs-lookup"><span data-stu-id="3d6b6-275">Invokes the action.</span></span> |

<span data-ttu-id="3d6b6-276">K poskytnutí vlastní implementace pro některá z těchto rozhraní použijte kolekci **Services** na objektu **HttpConfiguration** :</span><span class="sxs-lookup"><span data-stu-id="3d6b6-276">To provide your own implementation for any of these interfaces, use the **Services** collection on the **HttpConfiguration** object:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample11.cs)]
