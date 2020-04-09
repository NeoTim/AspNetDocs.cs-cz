---
uid: web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api
title: Směrování v ASP.NET webovém rozhraní API | Dokumenty společnosti Microsoft
author: MikeWasson
description: ''
ms.author: riande
ms.date: 10/29/2018
ms.assetid: 0675bdc7-282f-4f47-b7f3-7e02133940ca
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 85862c094cc54365267b1f21e68d235a15519cda
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676130"
---
# <a name="routing-in-aspnet-web-api"></a><span data-ttu-id="11980-102">Směrování v ASP.NET webovérozhraní API</span><span class="sxs-lookup"><span data-stu-id="11980-102">Routing in ASP.NET Web API</span></span>

<span data-ttu-id="11980-103">podle [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="11980-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="11980-104">Tento článek popisuje, jak ASP.NET webové rozhraní API směruje požadavky HTTP na řadiče.</span><span class="sxs-lookup"><span data-stu-id="11980-104">This article describes how ASP.NET Web API routes HTTP requests to controllers.</span></span>

> [!NOTE]
> <span data-ttu-id="11980-105">Pokud jste obeznámeni s ASP.NET MVC, směrování webového rozhraní API je velmi podobný směrování MVC.</span><span class="sxs-lookup"><span data-stu-id="11980-105">If you are familiar with ASP.NET MVC, Web API routing is very similar to MVC routing.</span></span> <span data-ttu-id="11980-106">Hlavní rozdíl spočá, že webové rozhraní API používá k výběru akce sloveso HTTP, nikoli cestu IDENTIFIKÁTORURI.</span><span class="sxs-lookup"><span data-stu-id="11980-106">The main difference is that Web API uses the HTTP verb, not the URI path, to select the action.</span></span> <span data-ttu-id="11980-107">Můžete také použít směrování ve stylu MVC ve webovém rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="11980-107">You can also use MVC-style routing in Web API.</span></span> <span data-ttu-id="11980-108">Tento článek nepředpokládá žádné znalosti ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="11980-108">This article does not assume any knowledge of ASP.NET MVC.</span></span>

## <a name="routing-tables"></a><span data-ttu-id="11980-109">Směrování tabulek</span><span class="sxs-lookup"><span data-stu-id="11980-109">Routing Tables</span></span>

<span data-ttu-id="11980-110">V ASP.NET webové rozhraní API je *řadič* třídou, která zpracovává požadavky HTTP.</span><span class="sxs-lookup"><span data-stu-id="11980-110">In ASP.NET Web API, a *controller* is a class that handles HTTP requests.</span></span> <span data-ttu-id="11980-111">Veřejné metody regulátoru se nazývají *akční metody* nebo jednoduše *akce*.</span><span class="sxs-lookup"><span data-stu-id="11980-111">The public methods of the controller are called *action methods* or simply *actions*.</span></span> <span data-ttu-id="11980-112">Když rozhraní webového rozhraní API obdrží požadavek, směruje požadavek na akci.</span><span class="sxs-lookup"><span data-stu-id="11980-112">When the Web API framework receives a request, it routes the request to an action.</span></span>

<span data-ttu-id="11980-113">Chcete-li zjistit, kterou akci vyvolat, rozhraní používá *směrovací tabulku*.</span><span class="sxs-lookup"><span data-stu-id="11980-113">To determine which action to invoke, the framework uses a *routing table*.</span></span> <span data-ttu-id="11980-114">Šablona projektu Visual Studia pro webové rozhraní API vytvoří výchozí trasu:</span><span class="sxs-lookup"><span data-stu-id="11980-114">The Visual Studio project template for Web API creates a default route:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="11980-115">Tato trasa je definována v *souboru WebApiConfig.cs,* který je umístěn v adresáři *Start\_aplikace:*</span><span class="sxs-lookup"><span data-stu-id="11980-115">This route is defined in the *WebApiConfig.cs* file, which is placed in the *App\_Start* directory:</span></span>

![](routing-in-aspnet-web-api/_static/image1.png)

<span data-ttu-id="11980-116">Další informace o `WebApiConfig` třídě naleznete v [tématu Configuring ASP.NET Web API](../advanced/configuring-aspnet-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="11980-116">For more information about the `WebApiConfig` class, see [Configuring ASP.NET Web API](../advanced/configuring-aspnet-web-api.md).</span></span>

<span data-ttu-id="11980-117">Pokud vlastní webapi, musíte nastavit směrovací tabulku `HttpSelfHostConfiguration` přímo na objektu.</span><span class="sxs-lookup"><span data-stu-id="11980-117">If you self-host Web API, you must set the routing table directly on the `HttpSelfHostConfiguration` object.</span></span> <span data-ttu-id="11980-118">Další informace naleznete [v tématu Self-Host a Web API](../older-versions/self-host-a-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="11980-118">For more information, see [Self-Host a Web API](../older-versions/self-host-a-web-api.md).</span></span>

<span data-ttu-id="11980-119">Každá položka ve směrovací tabulce obsahuje *šablonu postupu*.</span><span class="sxs-lookup"><span data-stu-id="11980-119">Each entry in the routing table contains a *route template*.</span></span> <span data-ttu-id="11980-120">Výchozí šablona trasy pro &quot;webové rozhraní API je api/{controller}/{id}&quot;.</span><span class="sxs-lookup"><span data-stu-id="11980-120">The default route template for Web API is &quot;api/{controller}/{id}&quot;.</span></span> <span data-ttu-id="11980-121">V této &quot;šabloně je rozhraní API&quot; segmentem cesty literálu a {controller} a {id} jsou zástupné proměnné.</span><span class="sxs-lookup"><span data-stu-id="11980-121">In this template, &quot;api&quot; is a literal path segment, and {controller} and {id} are placeholder variables.</span></span>

<span data-ttu-id="11980-122">Když rozhraní webového rozhraní API obdrží požadavek HTTP, pokusí se porovnat identifikátor URI s jednou ze šablon tras ve směrovací tabulce.</span><span class="sxs-lookup"><span data-stu-id="11980-122">When the Web API framework receives an HTTP request, it tries to match the URI against one of the route templates in the routing table.</span></span> <span data-ttu-id="11980-123">Pokud se neshoduje žádná trasa, klient obdrží chybu 404.</span><span class="sxs-lookup"><span data-stu-id="11980-123">If no route matches, the client receives a 404 error.</span></span> <span data-ttu-id="11980-124">Například následující identifikátory URI odpovídají výchozí trase:</span><span class="sxs-lookup"><span data-stu-id="11980-124">For example, the following URIs match the default route:</span></span>

- <span data-ttu-id="11980-125">/api/kontakty</span><span class="sxs-lookup"><span data-stu-id="11980-125">/api/contacts</span></span>
- <span data-ttu-id="11980-126">/api/kontakty/1</span><span class="sxs-lookup"><span data-stu-id="11980-126">/api/contacts/1</span></span>
- <span data-ttu-id="11980-127">/api/products/gizmo1</span><span class="sxs-lookup"><span data-stu-id="11980-127">/api/products/gizmo1</span></span>

<span data-ttu-id="11980-128">Následující identifikátor URI se však neshoduje, &quot;&quot; protože postrádá segment rozhraní API:</span><span class="sxs-lookup"><span data-stu-id="11980-128">However, the following URI does not match, because it lacks the &quot;api&quot; segment:</span></span>

- <span data-ttu-id="11980-129">/kontakty/1</span><span class="sxs-lookup"><span data-stu-id="11980-129">/contacts/1</span></span>

> [!NOTE]
> <span data-ttu-id="11980-130">Důvodem pro použití "api" v trase je, aby se zabránilo kolizím s ASP.NET směrování MVC.</span><span class="sxs-lookup"><span data-stu-id="11980-130">The reason for using "api" in the route is to avoid collisions with ASP.NET MVC routing.</span></span> <span data-ttu-id="11980-131">Tímto způsobem můžete &quot;mít&quot; /kontakty přejít na &quot;řadič MVC a /api/contacts&quot; přejít na řadič webového rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="11980-131">That way, you can have &quot;/contacts&quot; go to an MVC controller, and &quot;/api/contacts&quot; go to a Web API controller.</span></span> <span data-ttu-id="11980-132">Samozřejmě, pokud se vám nelíbí tato konvence, můžete změnit výchozí směrovací tabulku.</span><span class="sxs-lookup"><span data-stu-id="11980-132">Of course, if you don't like this convention, you can change the default route table.</span></span>

<span data-ttu-id="11980-133">Jakmile je nalezena odpovídající trasa, webové rozhraní API vybere řadič a akci:</span><span class="sxs-lookup"><span data-stu-id="11980-133">Once a matching route is found, Web API selects the controller and the action:</span></span>

- <span data-ttu-id="11980-134">Chcete-li najít řadič, &quot;&quot; webové rozhraní API přidá řadič k hodnotě proměnné *{controller}.*</span><span class="sxs-lookup"><span data-stu-id="11980-134">To find the controller, Web API adds &quot;Controller&quot; to the value of the *{controller}* variable.</span></span>
- <span data-ttu-id="11980-135">Chcete-li najít akci, webové rozhraní API se podívá na sloveso HTTP a pak vyhledá akci, jejíž název začíná tímto názvem slovesa HTTP.</span><span class="sxs-lookup"><span data-stu-id="11980-135">To find the action, Web API looks at the HTTP verb, and then looks for an action whose name begins with that HTTP verb name.</span></span> <span data-ttu-id="11980-136">Například s požadavkem GET webové rozhraní API &quot;hledá&quot;akci &quot;s&quot; předponou Get , například GetContact nebo &quot;GetAllContacts&quot;.</span><span class="sxs-lookup"><span data-stu-id="11980-136">For example, with a GET request, Web API looks for an action prefixed with &quot;Get&quot;, such as &quot;GetContact&quot; or &quot;GetAllContacts&quot;.</span></span> <span data-ttu-id="11980-137">Tato konvence se vztahuje pouze na get, post, put, delete, head, options a patch slovesa.</span><span class="sxs-lookup"><span data-stu-id="11980-137">This convention applies only to GET, POST, PUT, DELETE, HEAD, OPTIONS, and PATCH verbs.</span></span> <span data-ttu-id="11980-138">Ostatní slovesa PROTOKOLU HTTP můžete povolit pomocí atributů na řadiči.</span><span class="sxs-lookup"><span data-stu-id="11980-138">You can enable other HTTP verbs by using attributes on your controller.</span></span> <span data-ttu-id="11980-139">Příklad uvidíme později.</span><span class="sxs-lookup"><span data-stu-id="11980-139">We'll see an example of that later.</span></span>
- <span data-ttu-id="11980-140">Ostatní zástupné proměnné v šabloně trasy, například *{id},* jsou mapovány na parametry akce.</span><span class="sxs-lookup"><span data-stu-id="11980-140">Other placeholder variables in the route template, such as *{id},* are mapped to action parameters.</span></span>

<span data-ttu-id="11980-141">Pojďme se podívat na příklad.</span><span class="sxs-lookup"><span data-stu-id="11980-141">Let's look at an example.</span></span> <span data-ttu-id="11980-142">Předpokládejme, že definujete následující řadič:</span><span class="sxs-lookup"><span data-stu-id="11980-142">Suppose that you define the following controller:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample2.cs)]

<span data-ttu-id="11980-143">Zde jsou některé možné požadavky HTTP, spolu s akcí, která se vyvolá pro každý:</span><span class="sxs-lookup"><span data-stu-id="11980-143">Here are some possible HTTP requests, along with the action that gets invoked for each:</span></span>

| <span data-ttu-id="11980-144">Sloveso HTTP</span><span class="sxs-lookup"><span data-stu-id="11980-144">HTTP Verb</span></span> | <span data-ttu-id="11980-145">Cesta identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="11980-145">URI Path</span></span> | <span data-ttu-id="11980-146">Akce</span><span class="sxs-lookup"><span data-stu-id="11980-146">Action</span></span> | <span data-ttu-id="11980-147">Parametr</span><span class="sxs-lookup"><span data-stu-id="11980-147">Parameter</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="11980-148">GET</span><span class="sxs-lookup"><span data-stu-id="11980-148">GET</span></span> | <span data-ttu-id="11980-149">api/produkty</span><span class="sxs-lookup"><span data-stu-id="11980-149">api/products</span></span> | <span data-ttu-id="11980-150">GetAllProducts</span><span class="sxs-lookup"><span data-stu-id="11980-150">GetAllProducts</span></span> | <span data-ttu-id="11980-151">*(žádný)*</span><span class="sxs-lookup"><span data-stu-id="11980-151">*(none)*</span></span> |
| <span data-ttu-id="11980-152">GET</span><span class="sxs-lookup"><span data-stu-id="11980-152">GET</span></span> | <span data-ttu-id="11980-153">api/produkty/4</span><span class="sxs-lookup"><span data-stu-id="11980-153">api/products/4</span></span> | <span data-ttu-id="11980-154">GetProductById</span><span class="sxs-lookup"><span data-stu-id="11980-154">GetProductById</span></span> | <span data-ttu-id="11980-155">4</span><span class="sxs-lookup"><span data-stu-id="11980-155">4</span></span> |
| <span data-ttu-id="11980-156">DELETE</span><span class="sxs-lookup"><span data-stu-id="11980-156">DELETE</span></span> | <span data-ttu-id="11980-157">api/produkty/4</span><span class="sxs-lookup"><span data-stu-id="11980-157">api/products/4</span></span> | <span data-ttu-id="11980-158">Odstranit produkt</span><span class="sxs-lookup"><span data-stu-id="11980-158">DeleteProduct</span></span> | <span data-ttu-id="11980-159">4</span><span class="sxs-lookup"><span data-stu-id="11980-159">4</span></span> |
| <span data-ttu-id="11980-160">POST</span><span class="sxs-lookup"><span data-stu-id="11980-160">POST</span></span> | <span data-ttu-id="11980-161">api/produkty</span><span class="sxs-lookup"><span data-stu-id="11980-161">api/products</span></span> | <span data-ttu-id="11980-162">*(bez shody)*</span><span class="sxs-lookup"><span data-stu-id="11980-162">*(no match)*</span></span> |  |

<span data-ttu-id="11980-163">Všimněte si, že segment *{id}* identifikátoru URI, pokud je přítomen, je mapován na parametr *id* akce.</span><span class="sxs-lookup"><span data-stu-id="11980-163">Notice that the *{id}* segment of the URI, if present, is mapped to the *id* parameter of the action.</span></span> <span data-ttu-id="11980-164">V tomto příkladu řadič definuje dvě metody GET, jednu s parametrem *id* a jednu bez parametrů.</span><span class="sxs-lookup"><span data-stu-id="11980-164">In this example, the controller defines two GET methods, one with an *id* parameter and one with no parameters.</span></span>

<span data-ttu-id="11980-165">Všimněte si také, že požadavek POST se &quot;nezdaří, protože řadič nedefinuje Post... &quot; metodou.</span><span class="sxs-lookup"><span data-stu-id="11980-165">Also, note that the POST request will fail, because the controller does not define a &quot;Post...&quot; method.</span></span>

## <a name="routing-variations"></a><span data-ttu-id="11980-166">Varianty směrování</span><span class="sxs-lookup"><span data-stu-id="11980-166">Routing Variations</span></span>

<span data-ttu-id="11980-167">Předchozí část popisuje základní mechanismus směrování pro ASP.NET webové rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="11980-167">The previous section described the basic routing mechanism for ASP.NET Web API.</span></span> <span data-ttu-id="11980-168">Tato část popisuje některé varianty.</span><span class="sxs-lookup"><span data-stu-id="11980-168">This section describes some variations.</span></span>

### <a name="http-verbs"></a><span data-ttu-id="11980-169">Http slovesa</span><span class="sxs-lookup"><span data-stu-id="11980-169">HTTP verbs</span></span>

<span data-ttu-id="11980-170">Namísto použití konvence pojmenování pro slovesa HTTP můžete explicitně zadat sloveso HTTP pro akci zdobením metody akce jedním z následujících atributů:</span><span class="sxs-lookup"><span data-stu-id="11980-170">Instead of using the naming convention for HTTP verbs, you can explicitly specify the HTTP verb for an action by decorating the action method with one of the following attributes:</span></span>

- `[HttpGet]`
- `[HttpPut]`
- `[HttpPost]`
- `[HttpDelete]`
- `[HttpHead]`
- `[HttpOptions]`
- `[HttpPatch]`

<span data-ttu-id="11980-171">V následujícím příkladu `FindProduct` je metoda mapována na požadavky GET:</span><span class="sxs-lookup"><span data-stu-id="11980-171">In the following example, the `FindProduct` method is mapped to GET requests:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample3.cs)]

<span data-ttu-id="11980-172">Chcete-li povolit více sloves protokolu HTTP pro akci nebo povolit slovesa HTTP jiná než `[AcceptVerbs]` GET, PUT, POST, DELETE, HEAD, OPTIONS a PATCH, použijte atribut, který přebírá seznam sloves PROTOKOLU HTTP.</span><span class="sxs-lookup"><span data-stu-id="11980-172">To allow multiple HTTP verbs for an action, or to allow HTTP verbs other than GET, PUT, POST, DELETE, HEAD, OPTIONS, and PATCH, use the `[AcceptVerbs]` attribute, which takes a list of HTTP verbs.</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample4.cs)]

<a id="routing_by_action_name"></a>
### <a name="routing-by-action-name"></a><span data-ttu-id="11980-173">Směrování podle názvu akce</span><span class="sxs-lookup"><span data-stu-id="11980-173">Routing by Action Name</span></span>

<span data-ttu-id="11980-174">S výchozí šablonou směrování používá webové rozhraní API k výběru akce sloveso HTTP.</span><span class="sxs-lookup"><span data-stu-id="11980-174">With the default routing template, Web API uses the HTTP verb to select the action.</span></span> <span data-ttu-id="11980-175">Můžete však také vytvořit trasu, kde je název akce zahrnut v identifikátoru URI:</span><span class="sxs-lookup"><span data-stu-id="11980-175">However, you can also create a route where the action name is included in the URI:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample5.cs)]

<span data-ttu-id="11980-176">V této šabloně trasy pojmenuje parametr *{action}* metodu akce na řadiči.</span><span class="sxs-lookup"><span data-stu-id="11980-176">In this route template, the *{action}* parameter names the action method on the controller.</span></span> <span data-ttu-id="11980-177">Pomocí tohoto stylu směrování použijte atributy k určení povolených sloves PROTOKOLU HTTP.</span><span class="sxs-lookup"><span data-stu-id="11980-177">With this style of routing, use attributes to specify the allowed HTTP verbs.</span></span> <span data-ttu-id="11980-178">Předpokládejme například, že váš řadič má následující metodu:</span><span class="sxs-lookup"><span data-stu-id="11980-178">For example, suppose your controller has the following method:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample6.cs)]

<span data-ttu-id="11980-179">V tomto případě get požadavek na "api/products/details/1" by mapovat na metodu. `Details`</span><span class="sxs-lookup"><span data-stu-id="11980-179">In this case, a GET request for "api/products/details/1" would map to the `Details` method.</span></span> <span data-ttu-id="11980-180">Tento styl směrování je podobný ASP.NET MVC a může být vhodný pro rozhraní API ve stylu RPC.</span><span class="sxs-lookup"><span data-stu-id="11980-180">This style of routing is similar to ASP.NET MVC, and may be appropriate for an RPC-style API.</span></span>

<span data-ttu-id="11980-181">Název akce můžete přepsat pomocí `[ActionName]` atributu.</span><span class="sxs-lookup"><span data-stu-id="11980-181">You can override the action name by using the `[ActionName]` attribute.</span></span> <span data-ttu-id="11980-182">V následujícím příkladu jsou dvě akce, které mapují na &quot;api/products/thumbnail/*id*. Jeden podporuje GET a druhý podporuje POST:</span><span class="sxs-lookup"><span data-stu-id="11980-182">In the following example, there are two actions that map to &quot;api/products/thumbnail/*id*. One supports GET and the other supports POST:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample7.cs)]

### <a name="non-actions"></a><span data-ttu-id="11980-183">Neakce</span><span class="sxs-lookup"><span data-stu-id="11980-183">Non-Actions</span></span>

<span data-ttu-id="11980-184">Chcete-li zabránit vyvolání metody jako akce, použijte `[NonAction]` atribut.</span><span class="sxs-lookup"><span data-stu-id="11980-184">To prevent a method from getting invoked as an action, use the `[NonAction]` attribute.</span></span> <span data-ttu-id="11980-185">To signalizuje rámci, že metoda není akce, i v případě, že by jinak odpovídat pravidla směrování.</span><span class="sxs-lookup"><span data-stu-id="11980-185">This signals to the framework that the method is not an action, even if it would otherwise match the routing rules.</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample8.cs)]

## <a name="further-reading"></a><span data-ttu-id="11980-186">Další čtení</span><span class="sxs-lookup"><span data-stu-id="11980-186">Further Reading</span></span>

<span data-ttu-id="11980-187">Toto téma poskytlo zobrazení směrování na vysoké úrovni.</span><span class="sxs-lookup"><span data-stu-id="11980-187">This topic provided a high-level view of routing.</span></span> <span data-ttu-id="11980-188">Další podrobnosti naleznete v [tématu Směrování a výběr akce](routing-and-action-selection.md), který přesně popisuje, jak rozhraní odpovídá uri na trasu, vybere řadič a potom vybere akci vyvolat.</span><span class="sxs-lookup"><span data-stu-id="11980-188">For more detail, see [Routing and Action Selection](routing-and-action-selection.md), which describes exactly how the framework matches a URI to a route, selects a controller, and then selects the action to invoke.</span></span>
