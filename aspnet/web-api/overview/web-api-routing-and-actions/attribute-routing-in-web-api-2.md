---
uid: web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2
title: Směrování atributů v rozhraní API ASP.NET Web API 2 | Dokumenty společnosti Microsoft
author: MikeWasson
description: ''
ms.author: riande
ms.date: 01/20/2014
ms.assetid: 979d6c9f-0129-4e5b-ae56-4507b281b86d
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2
msc.type: authoredcontent
ms.openlocfilehash: bb68fe8e6769619029a3fa039d6f0d6f3303afbe
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675388"
---
# <a name="attribute-routing-in-aspnet-web-api-2"></a><span data-ttu-id="637c0-102">Směrování atributů v ASP.NET webovérozhraní API 2</span><span class="sxs-lookup"><span data-stu-id="637c0-102">Attribute Routing in ASP.NET Web API 2</span></span>

<span data-ttu-id="637c0-103">podle [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="637c0-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="637c0-104">*Směrování* je způsob, jakým webové rozhraní API odpovídá identifikátoru URI akci.</span><span class="sxs-lookup"><span data-stu-id="637c0-104">*Routing* is how Web API matches a URI to an action.</span></span> <span data-ttu-id="637c0-105">Webové rozhraní API 2 podporuje nový typ směrování, nazývaný *směrování atributů*.</span><span class="sxs-lookup"><span data-stu-id="637c0-105">Web API 2 supports a new type of routing, called *attribute routing*.</span></span> <span data-ttu-id="637c0-106">Jak název napovídá, směrování atributů používá k definování tras atributy.</span><span class="sxs-lookup"><span data-stu-id="637c0-106">As the name implies, attribute routing uses attributes to define routes.</span></span> <span data-ttu-id="637c0-107">Směrování atributů poskytuje větší kontrolu nad identifikátory URI ve webovém rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="637c0-107">Attribute routing gives you more control over the URIs in your web API.</span></span> <span data-ttu-id="637c0-108">Můžete například snadno vytvořit identifikátory URI, které popisují hierarchie prostředků.</span><span class="sxs-lookup"><span data-stu-id="637c0-108">For example, you can easily create URIs that describe hierarchies of resources.</span></span>

<span data-ttu-id="637c0-109">Dřívější styl směrování, nazývaný směrování založený na konvencích, je stále plně podporován.</span><span class="sxs-lookup"><span data-stu-id="637c0-109">The earlier style of routing, called convention-based routing, is still fully supported.</span></span> <span data-ttu-id="637c0-110">Ve skutečnosti můžete kombinovat obě techniky ve stejném projektu.</span><span class="sxs-lookup"><span data-stu-id="637c0-110">In fact, you can combine both techniques in the same project.</span></span>

<span data-ttu-id="637c0-111">Toto téma ukazuje, jak povolit směrování atributů a popisuje různé možnosti směrování atributů.</span><span class="sxs-lookup"><span data-stu-id="637c0-111">This topic shows how to enable attribute routing and describes the various options for attribute routing.</span></span> <span data-ttu-id="637c0-112">Kurz na konci výuky, která používá směrování atributů, najdete [v tématu Vytvoření rozhraní REST API s směrováním atributů ve webovém rozhraní API 2](create-a-rest-api-with-attribute-routing.md).</span><span class="sxs-lookup"><span data-stu-id="637c0-112">For an end-to-end tutorial that uses attribute routing, see [Create a REST API with Attribute Routing in Web API 2](create-a-rest-api-with-attribute-routing.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="637c0-113">Požadavky</span><span class="sxs-lookup"><span data-stu-id="637c0-113">Prerequisites</span></span>

<span data-ttu-id="637c0-114">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Verze Společenství, Professional nebo Enterprise</span><span class="sxs-lookup"><span data-stu-id="637c0-114">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community, Professional, or Enterprise edition</span></span>

<span data-ttu-id="637c0-115">Případně použijte NuGet Správce balíčků k instalaci potřebných balíčků.</span><span class="sxs-lookup"><span data-stu-id="637c0-115">Alternatively, use NuGet Package Manager to install the necessary packages.</span></span> <span data-ttu-id="637c0-116">V nabídce **Nástroje** v sadě Visual Studio vyberte **Položku Správce balíčků NuGet**a potom vyberte **konzolu správce balíčků**.</span><span class="sxs-lookup"><span data-stu-id="637c0-116">From the **Tools** menu in Visual Studio, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="637c0-117">V okně Konzoly správce balíčků zadejte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="637c0-117">Enter the following command in the Package Manager Console window:</span></span>

`Install-Package Microsoft.AspNet.WebApi.WebHost`

<a id="why"></a>
## <a name="why-attribute-routing"></a><span data-ttu-id="637c0-118">Proč směrování atributů?</span><span class="sxs-lookup"><span data-stu-id="637c0-118">Why Attribute Routing?</span></span>

<span data-ttu-id="637c0-119">První vydání webového rozhraní API používá směrování *založené na konvencích.*</span><span class="sxs-lookup"><span data-stu-id="637c0-119">The first release of Web API used *convention-based* routing.</span></span> <span data-ttu-id="637c0-120">V tomto typu směrování definujete jednu nebo více šablon tras, které jsou v podstatě parametrizované řetězce.</span><span class="sxs-lookup"><span data-stu-id="637c0-120">In that type of routing, you define one or more route templates, which are basically parameterized strings.</span></span> <span data-ttu-id="637c0-121">Když rozhraní obdrží požadavek, odpovídá identifikátoru URI proti šabloně trasy.</span><span class="sxs-lookup"><span data-stu-id="637c0-121">When the framework receives a request, it matches the URI against the route template.</span></span> <span data-ttu-id="637c0-122">Další informace o směrování založeném na konvencích naleznete [v tématu Směrování v ASP.NET webovérozhraní API](routing-in-aspnet-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="637c0-122">For more information about convention-based routing, see [Routing in ASP.NET Web API](routing-in-aspnet-web-api.md).</span></span>

<span data-ttu-id="637c0-123">Jednou z výhod směrování na základě konvence je, že šablony jsou definovány na jednom místě a pravidla směrování jsou použity konzistentně ve všech řadičích.</span><span class="sxs-lookup"><span data-stu-id="637c0-123">One advantage of convention-based routing is that templates are defined in a single place, and the routing rules are applied consistently across all controllers.</span></span> <span data-ttu-id="637c0-124">Bohužel směrování založené na konvencích ztěžuje podporu určitých vzorů URI, které jsou běžné v restful api.</span><span class="sxs-lookup"><span data-stu-id="637c0-124">Unfortunately, convention-based routing makes it hard to support certain URI patterns that are common in RESTful APIs.</span></span> <span data-ttu-id="637c0-125">Například zdroje často obsahují podřízené prostředky: Zákazníci mají objednávky, filmy mají herce, knihy mají autory a tak dále.</span><span class="sxs-lookup"><span data-stu-id="637c0-125">For example, resources often contain child resources: Customers have orders, movies have actors, books have authors, and so forth.</span></span> <span data-ttu-id="637c0-126">Je přirozené vytvářet identifikátory URI, které odrážejí tyto vztahy:</span><span class="sxs-lookup"><span data-stu-id="637c0-126">It's natural to create URIs that reflect these relations:</span></span>

`/customers/1/orders`

<span data-ttu-id="637c0-127">Tento typ identifikátoru URI je obtížné vytvořit pomocí směrování založeného na konvencích.</span><span class="sxs-lookup"><span data-stu-id="637c0-127">This type of URI is difficult to create using convention-based routing.</span></span> <span data-ttu-id="637c0-128">I když to lze provést, výsledky nejsou škálovat dobře, pokud máte mnoho řadičů nebo typů prostředků.</span><span class="sxs-lookup"><span data-stu-id="637c0-128">Although it can be done, the results don't scale well if you have many controllers or resource types.</span></span>

<span data-ttu-id="637c0-129">Při směrování atributů je triviální definovat trasu pro tento identifikátor URI.</span><span class="sxs-lookup"><span data-stu-id="637c0-129">With attribute routing, it's trivial to define a route for this URI.</span></span> <span data-ttu-id="637c0-130">Jednoduše přidáte atribut do akce kontroleru:</span><span class="sxs-lookup"><span data-stu-id="637c0-130">You simply add an attribute to the controller action:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample1.cs)]

<span data-ttu-id="637c0-131">Zde jsou některé další vzory, které atribut směrování usnadňuje.</span><span class="sxs-lookup"><span data-stu-id="637c0-131">Here are some other patterns that attribute routing makes easy.</span></span>

<span data-ttu-id="637c0-132">**Správa verzí rozhraní API**</span><span class="sxs-lookup"><span data-stu-id="637c0-132">**API versioning**</span></span>

<span data-ttu-id="637c0-133">V tomto příkladu "/api/v1/products" by být směrovány do jiného řadiče než "/api/v2/products".</span><span class="sxs-lookup"><span data-stu-id="637c0-133">In this example, "/api/v1/products" would be routed to a different controller than "/api/v2/products".</span></span>

`/api/v1/products`
`/api/v2/products`

<span data-ttu-id="637c0-134">**Přetížené segmenty IDENTIFIKÁTORŮ URI**</span><span class="sxs-lookup"><span data-stu-id="637c0-134">**Overloaded URI segments**</span></span>

<span data-ttu-id="637c0-135">V tomto příkladu "1" je číslo objednávky, ale "čekající" mapuje na kolekci.</span><span class="sxs-lookup"><span data-stu-id="637c0-135">In this example, "1" is an order number, but "pending" maps to a collection.</span></span>

`/orders/1`
`/orders/pending`

<span data-ttu-id="637c0-136">**Více typů parametrů**</span><span class="sxs-lookup"><span data-stu-id="637c0-136">**Multiple parameter types**</span></span>

<span data-ttu-id="637c0-137">V tomto příkladu je "1" číslo objednávky, ale "2013/06/16" určuje datum.</span><span class="sxs-lookup"><span data-stu-id="637c0-137">In this example, "1" is an order number, but "2013/06/16" specifies a date.</span></span>

`/orders/1`
`/orders/2013/06/16`

<a id="enable"></a>
## <a name="enabling-attribute-routing"></a><span data-ttu-id="637c0-138">Povolení směrování atributů</span><span class="sxs-lookup"><span data-stu-id="637c0-138">Enabling Attribute Routing</span></span>

<span data-ttu-id="637c0-139">Chcete-li povolit směrování atributů, zavolejte **maphttpattributeroutes** během konfigurace.</span><span class="sxs-lookup"><span data-stu-id="637c0-139">To enable attribute routing, call **MapHttpAttributeRoutes** during configuration.</span></span> <span data-ttu-id="637c0-140">Tato metoda rozšíření je definována ve třídě **System.Web.Http.HttpConfigurationExtensions.**</span><span class="sxs-lookup"><span data-stu-id="637c0-140">This extension method is defined in the **System.Web.Http.HttpConfigurationExtensions** class.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample2.cs)]

<span data-ttu-id="637c0-141">Směrování atributů lze kombinovat s [směrováním založeným na konvencích.](routing-in-aspnet-web-api.md)</span><span class="sxs-lookup"><span data-stu-id="637c0-141">Attribute routing can be combined with [convention-based](routing-in-aspnet-web-api.md) routing.</span></span> <span data-ttu-id="637c0-142">Chcete-li definovat trasy založené na konvencích, zavolejte metodu **MapHttpRoute.**</span><span class="sxs-lookup"><span data-stu-id="637c0-142">To define convention-based routes, call the **MapHttpRoute** method.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample3.cs)]

<span data-ttu-id="637c0-143">Další informace o konfiguraci webového rozhraní API naleznete [v tématu Konfigurace ASP.NET webovérozhraní API 2](../advanced/configuring-aspnet-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="637c0-143">For more information about configuring Web API, see [Configuring ASP.NET Web API 2](../advanced/configuring-aspnet-web-api.md).</span></span>

<a id="config"></a>
### <a name="note-migrating-from-web-api-1"></a><span data-ttu-id="637c0-144">Poznámka: Migrace z webového rozhraní API 1</span><span class="sxs-lookup"><span data-stu-id="637c0-144">Note: Migrating From Web API 1</span></span>

<span data-ttu-id="637c0-145">Před web api 2 šablony projektu webového rozhraní API generované kód, jako je tento:</span><span class="sxs-lookup"><span data-stu-id="637c0-145">Prior to Web API 2, the Web API project templates generated code like this:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample4.cs)]

<span data-ttu-id="637c0-146">Pokud je povoleno směrování atributů, tento kód vyvolá výjimku.</span><span class="sxs-lookup"><span data-stu-id="637c0-146">If attribute routing is enabled, this code will throw an exception.</span></span> <span data-ttu-id="637c0-147">Pokud inovujete existující projekt webového rozhraní API tak, aby používal směrování atributů, nezapomeňte aktualizovat tento konfigurační kód na následující:</span><span class="sxs-lookup"><span data-stu-id="637c0-147">If you upgrade an existing Web API project to use attribute routing, make sure to update this configuration code to the following:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample5.cs?highlight=4)]

> [!NOTE]
> <span data-ttu-id="637c0-148">Další informace naleznete [v tématu Konfigurace webového rozhraní API pomocí ASP.NET hostování](../advanced/configuring-aspnet-web-api.md#webhost).</span><span class="sxs-lookup"><span data-stu-id="637c0-148">For more information, see [Configuring Web API with ASP.NET Hosting](../advanced/configuring-aspnet-web-api.md#webhost).</span></span>

<a id="add-routes"></a>
## <a name="adding-route-attributes"></a><span data-ttu-id="637c0-149">Přidání atributů postupu</span><span class="sxs-lookup"><span data-stu-id="637c0-149">Adding Route Attributes</span></span>

<span data-ttu-id="637c0-150">Zde je příklad trasy definované pomocí atributu:</span><span class="sxs-lookup"><span data-stu-id="637c0-150">Here is an example of a route defined using an attribute:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample6.cs)]

<span data-ttu-id="637c0-151">Řetězec &quot;zákazníci/{customerId}/orders&quot; je šablona IDENTIFIKÁTORU URI pro trasu.</span><span class="sxs-lookup"><span data-stu-id="637c0-151">The string &quot;customers/{customerId}/orders&quot; is the URI template for the route.</span></span> <span data-ttu-id="637c0-152">Webové rozhraní API se pokusí porovnat identifikátor URI požadavku se šablonou.</span><span class="sxs-lookup"><span data-stu-id="637c0-152">Web API tries to match the request URI to the template.</span></span> <span data-ttu-id="637c0-153">V tomto příkladu "zákazníci" a "objednávky" jsou literálové segmenty a "{customerId}" je proměnný parametr.</span><span class="sxs-lookup"><span data-stu-id="637c0-153">In this example, "customers" and "orders" are literal segments, and "{customerId}" is a variable parameter.</span></span> <span data-ttu-id="637c0-154">Následující identifikátory URI by odpovídaly této šabloně:</span><span class="sxs-lookup"><span data-stu-id="637c0-154">The following URIs would match this template:</span></span>

- `http://localhost/customers/1/orders`
- `http://localhost/customers/bob/orders`
- `http://localhost/customers/1234-5678/orders`

<span data-ttu-id="637c0-155">Párování můžete omezit pomocí [omezení popsaných](#constraints)dále v tomto tématu.</span><span class="sxs-lookup"><span data-stu-id="637c0-155">You can restrict the matching by using [constraints](#constraints), described later in this topic.</span></span>

<span data-ttu-id="637c0-156">Všimněte &quot;si, že&quot; parametr {customerId} v šabloně postupu odpovídá názvu parametru *CustomerId* v metodě.</span><span class="sxs-lookup"><span data-stu-id="637c0-156">Notice that the &quot;{customerId}&quot; parameter in the route template matches the name of the *customerId* parameter in the method.</span></span> <span data-ttu-id="637c0-157">Když webové rozhraní API vyvolá akci řadiče, pokusí se svázat parametry trasy.</span><span class="sxs-lookup"><span data-stu-id="637c0-157">When Web API invokes the controller action, it tries to bind the route parameters.</span></span> <span data-ttu-id="637c0-158">Například pokud identifikátor `http://example.com/customers/1/orders`URI je , webové rozhraní API se pokusí svázat hodnotu "1" na *customerId* parametr v akci.</span><span class="sxs-lookup"><span data-stu-id="637c0-158">For example, if the URI is `http://example.com/customers/1/orders`, Web API tries to bind the value "1" to the *customerId* parameter in the action.</span></span>

<span data-ttu-id="637c0-159">Šablona identifikátoru URI může mít několik parametrů:</span><span class="sxs-lookup"><span data-stu-id="637c0-159">A URI template can have several parameters:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample7.cs)]

<span data-ttu-id="637c0-160">Všechny metody kontroleru, které nemají atribut trasy, používají směrování založené na konvencích.</span><span class="sxs-lookup"><span data-stu-id="637c0-160">Any controller methods that do not have a route attribute use convention-based routing.</span></span> <span data-ttu-id="637c0-161">Tímto způsobem můžete kombinovat oba typy směrování ve stejném projektu.</span><span class="sxs-lookup"><span data-stu-id="637c0-161">That way, you can combine both types of routing in the same project.</span></span>

## <a name="http-methods"></a><span data-ttu-id="637c0-162">Metody PROTOKOLU HTTP</span><span class="sxs-lookup"><span data-stu-id="637c0-162">HTTP Methods</span></span>

<span data-ttu-id="637c0-163">Webové rozhraní API také vybírá akce na základě metody HTTP požadavku (GET, POST atd.).</span><span class="sxs-lookup"><span data-stu-id="637c0-163">Web API also selects actions based on the HTTP method of the request (GET, POST, etc).</span></span> <span data-ttu-id="637c0-164">Ve výchozím nastavení webové rozhraní API hledá shodu bez rozlišování velkých a malých písmen se začátkem názvu metody řadiče.</span><span class="sxs-lookup"><span data-stu-id="637c0-164">By default, Web API looks for a case-insensitive match with the start of the controller method name.</span></span> <span data-ttu-id="637c0-165">Například metoda řadiče `PutCustomers` s názvem odpovídá požadavku HTTP PUT.</span><span class="sxs-lookup"><span data-stu-id="637c0-165">For example, a controller method named `PutCustomers` matches an HTTP PUT request.</span></span>

<span data-ttu-id="637c0-166">Tuto konvenci můžete přepsat zdobením metody následujícími atributy:</span><span class="sxs-lookup"><span data-stu-id="637c0-166">You can override this convention by decorating the method with any the following attributes:</span></span>

- <span data-ttu-id="637c0-167">**[HttpDelete]**</span><span class="sxs-lookup"><span data-stu-id="637c0-167">**[HttpDelete]**</span></span>
- <span data-ttu-id="637c0-168">**[HttpGet]**</span><span class="sxs-lookup"><span data-stu-id="637c0-168">**[HttpGet]**</span></span>
- <span data-ttu-id="637c0-169">**To je v pořádku.**</span><span class="sxs-lookup"><span data-stu-id="637c0-169">**[HttpHead]**</span></span>
- <span data-ttu-id="637c0-170">**[HttpOptions]**</span><span class="sxs-lookup"><span data-stu-id="637c0-170">**[HttpOptions]**</span></span>
- <span data-ttu-id="637c0-171">**[HttpPatch]**</span><span class="sxs-lookup"><span data-stu-id="637c0-171">**[HttpPatch]**</span></span>
- <span data-ttu-id="637c0-172">**[HttpPost]**</span><span class="sxs-lookup"><span data-stu-id="637c0-172">**[HttpPost]**</span></span>
- <span data-ttu-id="637c0-173">**[HttpPut]**</span><span class="sxs-lookup"><span data-stu-id="637c0-173">**[HttpPut]**</span></span>

<span data-ttu-id="637c0-174">Následující příklad mapuje metodu CreateBook na požadavky HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="637c0-174">The following example maps the CreateBook method to HTTP POST requests.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample8.cs)]

<span data-ttu-id="637c0-175">Pro všechny ostatní metody HTTP, včetně nestandardních metod, použijte atribut **AcceptVerbs,** který přebírá seznam metod HTTP.</span><span class="sxs-lookup"><span data-stu-id="637c0-175">For all other HTTP methods, including non-standard methods, use the **AcceptVerbs** attribute, which takes a list of HTTP methods.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample9.cs)]

<a id="prefixes"></a>
## <a name="route-prefixes"></a><span data-ttu-id="637c0-176">Předpony trasy</span><span class="sxs-lookup"><span data-stu-id="637c0-176">Route Prefixes</span></span>

<span data-ttu-id="637c0-177">Trasy v kontroleru často začínají stejnou předponou.</span><span class="sxs-lookup"><span data-stu-id="637c0-177">Often, the routes in a controller all start with the same prefix.</span></span> <span data-ttu-id="637c0-178">Příklad:</span><span class="sxs-lookup"><span data-stu-id="637c0-178">For example:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample10.cs)]

<span data-ttu-id="637c0-179">Běžnou předponu pro celý řadič můžete nastavit pomocí atributu **[RoutePrefix]:**</span><span class="sxs-lookup"><span data-stu-id="637c0-179">You can set a common prefix for an entire controller by using the **[RoutePrefix]** attribute:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample11.cs)]

<span data-ttu-id="637c0-180">K přepsání předpony trasy použijte vlnovku (~) v atributu metody:</span><span class="sxs-lookup"><span data-stu-id="637c0-180">Use a tilde (~) on the method attribute to override the route prefix:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample12.cs)]

<span data-ttu-id="637c0-181">Předpona trasy může obsahovat parametry:</span><span class="sxs-lookup"><span data-stu-id="637c0-181">The route prefix can include parameters:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample13.cs)]

<a id="constraints"></a>
## <a name="route-constraints"></a><span data-ttu-id="637c0-182">Omezení postupu</span><span class="sxs-lookup"><span data-stu-id="637c0-182">Route Constraints</span></span>

<span data-ttu-id="637c0-183">Omezení trasy umožňují omezit způsob, jakým jsou parametry v šabloně trasy spárovány.</span><span class="sxs-lookup"><span data-stu-id="637c0-183">Route constraints let you restrict how the parameters in the route template are matched.</span></span> <span data-ttu-id="637c0-184">Obecná syntaxe &quot;je {parameter:constraint}&quot;.</span><span class="sxs-lookup"><span data-stu-id="637c0-184">The general syntax is &quot;{parameter:constraint}&quot;.</span></span> <span data-ttu-id="637c0-185">Příklad:</span><span class="sxs-lookup"><span data-stu-id="637c0-185">For example:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample14.cs)]

<span data-ttu-id="637c0-186">Zde bude vybrána první trasa &quot;pouze&quot; v případě, že segment id identifikátoru URI je celé číslo.</span><span class="sxs-lookup"><span data-stu-id="637c0-186">Here, the first route will only be selected if the &quot;id&quot; segment of the URI is an integer.</span></span> <span data-ttu-id="637c0-187">V opačném případě bude zvolena druhá trasa.</span><span class="sxs-lookup"><span data-stu-id="637c0-187">Otherwise, the second route will be chosen.</span></span>

<span data-ttu-id="637c0-188">V následující tabulce jsou uvedena omezení, která jsou podporována.</span><span class="sxs-lookup"><span data-stu-id="637c0-188">The following table lists the constraints that are supported.</span></span>

| <span data-ttu-id="637c0-189">Omezení</span><span class="sxs-lookup"><span data-stu-id="637c0-189">Constraint</span></span> | <span data-ttu-id="637c0-190">Popis</span><span class="sxs-lookup"><span data-stu-id="637c0-190">Description</span></span> | <span data-ttu-id="637c0-191">Příklad</span><span class="sxs-lookup"><span data-stu-id="637c0-191">Example</span></span> |
| --- | --- | --- |
| <span data-ttu-id="637c0-192">alpha</span><span class="sxs-lookup"><span data-stu-id="637c0-192">alpha</span></span> | <span data-ttu-id="637c0-193">Odpovídá velkým nebo velkým písmenům latinky (a-z, A-Z)</span><span class="sxs-lookup"><span data-stu-id="637c0-193">Matches uppercase or lowercase Latin alphabet characters (a-z, A-Z)</span></span> | <span data-ttu-id="637c0-194">{x:alfa}</span><span class="sxs-lookup"><span data-stu-id="637c0-194">{x:alpha}</span></span> |
| <span data-ttu-id="637c0-195">bool</span><span class="sxs-lookup"><span data-stu-id="637c0-195">bool</span></span> | <span data-ttu-id="637c0-196">Odpovídá logické hodnotě.</span><span class="sxs-lookup"><span data-stu-id="637c0-196">Matches a Boolean value.</span></span> | <span data-ttu-id="637c0-197">{x:bool}</span><span class="sxs-lookup"><span data-stu-id="637c0-197">{x:bool}</span></span> |
| <span data-ttu-id="637c0-198">datetime</span><span class="sxs-lookup"><span data-stu-id="637c0-198">datetime</span></span> | <span data-ttu-id="637c0-199">Odpovídá hodnotě **DateTime.**</span><span class="sxs-lookup"><span data-stu-id="637c0-199">Matches a **DateTime** value.</span></span> | <span data-ttu-id="637c0-200">{x:datetime}</span><span class="sxs-lookup"><span data-stu-id="637c0-200">{x:datetime}</span></span> |
| <span data-ttu-id="637c0-201">decimal</span><span class="sxs-lookup"><span data-stu-id="637c0-201">decimal</span></span> | <span data-ttu-id="637c0-202">Odpovídá desítkové hodnotě.</span><span class="sxs-lookup"><span data-stu-id="637c0-202">Matches a decimal value.</span></span> | <span data-ttu-id="637c0-203">{x:desítkové}</span><span class="sxs-lookup"><span data-stu-id="637c0-203">{x:decimal}</span></span> |
| <span data-ttu-id="637c0-204">double</span><span class="sxs-lookup"><span data-stu-id="637c0-204">double</span></span> | <span data-ttu-id="637c0-205">Odpovídá 64bitové hodnotě s plovoucí desetinnou tácek.</span><span class="sxs-lookup"><span data-stu-id="637c0-205">Matches a 64-bit floating-point value.</span></span> | <span data-ttu-id="637c0-206">{x:double}</span><span class="sxs-lookup"><span data-stu-id="637c0-206">{x:double}</span></span> |
| <span data-ttu-id="637c0-207">float</span><span class="sxs-lookup"><span data-stu-id="637c0-207">float</span></span> | <span data-ttu-id="637c0-208">Odpovídá 32bitové hodnotě s plovoucí desetinnou hodnotou.</span><span class="sxs-lookup"><span data-stu-id="637c0-208">Matches a 32-bit floating-point value.</span></span> | <span data-ttu-id="637c0-209">{x:float}</span><span class="sxs-lookup"><span data-stu-id="637c0-209">{x:float}</span></span> |
| <span data-ttu-id="637c0-210">Identifikátor guid</span><span class="sxs-lookup"><span data-stu-id="637c0-210">guid</span></span> | <span data-ttu-id="637c0-211">Odpovídá hodnotě GUID.</span><span class="sxs-lookup"><span data-stu-id="637c0-211">Matches a GUID value.</span></span> | <span data-ttu-id="637c0-212">{x:guid}</span><span class="sxs-lookup"><span data-stu-id="637c0-212">{x:guid}</span></span> |
| <span data-ttu-id="637c0-213">int</span><span class="sxs-lookup"><span data-stu-id="637c0-213">int</span></span> | <span data-ttu-id="637c0-214">Odpovídá 32bitové celočíselné hodnotě.</span><span class="sxs-lookup"><span data-stu-id="637c0-214">Matches a 32-bit integer value.</span></span> | <span data-ttu-id="637c0-215">{x:int}</span><span class="sxs-lookup"><span data-stu-id="637c0-215">{x:int}</span></span> |
| <span data-ttu-id="637c0-216">length</span><span class="sxs-lookup"><span data-stu-id="637c0-216">length</span></span> | <span data-ttu-id="637c0-217">Odpovídá řetězci se zadanou délkou nebo v zadaném rozsahu délek.</span><span class="sxs-lookup"><span data-stu-id="637c0-217">Matches a string with the specified length or within a specified range of lengths.</span></span> | <span data-ttu-id="637c0-218">{x:délka(6)} {x:délka (1,20)}</span><span class="sxs-lookup"><span data-stu-id="637c0-218">{x:length(6)} {x:length(1,20)}</span></span> |
| <span data-ttu-id="637c0-219">long</span><span class="sxs-lookup"><span data-stu-id="637c0-219">long</span></span> | <span data-ttu-id="637c0-220">Odpovídá 64bitové celočíselné hodnotě.</span><span class="sxs-lookup"><span data-stu-id="637c0-220">Matches a 64-bit integer value.</span></span> | <span data-ttu-id="637c0-221">{x:long}</span><span class="sxs-lookup"><span data-stu-id="637c0-221">{x:long}</span></span> |
| <span data-ttu-id="637c0-222">max</span><span class="sxs-lookup"><span data-stu-id="637c0-222">max</span></span> | <span data-ttu-id="637c0-223">Odpovídá celé číslo s maximální hodnotou.</span><span class="sxs-lookup"><span data-stu-id="637c0-223">Matches an integer with a maximum value.</span></span> | <span data-ttu-id="637c0-224">{x:max(10)}</span><span class="sxs-lookup"><span data-stu-id="637c0-224">{x:max(10)}</span></span> |
| <span data-ttu-id="637c0-225">Maxlength</span><span class="sxs-lookup"><span data-stu-id="637c0-225">maxlength</span></span> | <span data-ttu-id="637c0-226">Odpovídá řetězci s maximální délkou.</span><span class="sxs-lookup"><span data-stu-id="637c0-226">Matches a string with a maximum length.</span></span> | <span data-ttu-id="637c0-227">{x:maxlength(10)}</span><span class="sxs-lookup"><span data-stu-id="637c0-227">{x:maxlength(10)}</span></span> |
| <span data-ttu-id="637c0-228">min</span><span class="sxs-lookup"><span data-stu-id="637c0-228">min</span></span> | <span data-ttu-id="637c0-229">Odpovídá celé číslo s minimální hodnotou.</span><span class="sxs-lookup"><span data-stu-id="637c0-229">Matches an integer with a minimum value.</span></span> | <span data-ttu-id="637c0-230">{x:min(10)}</span><span class="sxs-lookup"><span data-stu-id="637c0-230">{x:min(10)}</span></span> |
| <span data-ttu-id="637c0-231">Minlength</span><span class="sxs-lookup"><span data-stu-id="637c0-231">minlength</span></span> | <span data-ttu-id="637c0-232">Odpovídá řetězci s minimální délkou.</span><span class="sxs-lookup"><span data-stu-id="637c0-232">Matches a string with a minimum length.</span></span> | <span data-ttu-id="637c0-233">{x:minlength(10)}</span><span class="sxs-lookup"><span data-stu-id="637c0-233">{x:minlength(10)}</span></span> |
| <span data-ttu-id="637c0-234">range</span><span class="sxs-lookup"><span data-stu-id="637c0-234">range</span></span> | <span data-ttu-id="637c0-235">Odpovídá celé číslo v rozsahu hodnot.</span><span class="sxs-lookup"><span data-stu-id="637c0-235">Matches an integer within a range of values.</span></span> | <span data-ttu-id="637c0-236">{x:rozsah (10,50)}</span><span class="sxs-lookup"><span data-stu-id="637c0-236">{x:range(10,50)}</span></span> |
| <span data-ttu-id="637c0-237">Regex</span><span class="sxs-lookup"><span data-stu-id="637c0-237">regex</span></span> | <span data-ttu-id="637c0-238">Odpovídá regulárnímu výrazu.</span><span class="sxs-lookup"><span data-stu-id="637c0-238">Matches a regular expression.</span></span> | <span data-ttu-id="637c0-239">{x:regex(^\d{3}-\d{3}-\d{4}_)}</span><span class="sxs-lookup"><span data-stu-id="637c0-239">{x:regex(^\d{3}-\d{3}-\d{4}$)}</span></span> |

<span data-ttu-id="637c0-240">Všimněte si, že některá &quot;omezení, například min&quot;, přijmout argumenty v závorce.</span><span class="sxs-lookup"><span data-stu-id="637c0-240">Notice that some of the constraints, such as &quot;min&quot;, take arguments in parentheses.</span></span> <span data-ttu-id="637c0-241">Na parametr oddělený dvojtečkou můžete použít více omezení.</span><span class="sxs-lookup"><span data-stu-id="637c0-241">You can apply multiple constraints to a parameter, separated by a colon.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample15.cs)]

### <a name="custom-route-constraints"></a><span data-ttu-id="637c0-242">Vlastní omezení postupu</span><span class="sxs-lookup"><span data-stu-id="637c0-242">Custom Route Constraints</span></span>

<span data-ttu-id="637c0-243">Vlastní omezení trasy můžete vytvořit implementací rozhraní **IHttpRouteConstraint.**</span><span class="sxs-lookup"><span data-stu-id="637c0-243">You can create custom route constraints by implementing the **IHttpRouteConstraint** interface.</span></span> <span data-ttu-id="637c0-244">Například následující omezení omezuje parametr na nenulovou celočíselnou hodnotu.</span><span class="sxs-lookup"><span data-stu-id="637c0-244">For example, the following constraint restricts a parameter to a non-zero integer value.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample16.cs)]

<span data-ttu-id="637c0-245">Následující kód ukazuje, jak zaregistrovat omezení:</span><span class="sxs-lookup"><span data-stu-id="637c0-245">The following code shows how to register the constraint:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample17.cs)]

<span data-ttu-id="637c0-246">Nyní můžete použít omezení ve svých trasách:</span><span class="sxs-lookup"><span data-stu-id="637c0-246">Now you can apply the constraint in your routes:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample18.cs)]

<span data-ttu-id="637c0-247">Můžete také nahradit celou třídu **DefaultInlineConstraintResolver** implementací rozhraní **IInlineConstraintResolver.**</span><span class="sxs-lookup"><span data-stu-id="637c0-247">You can also replace the entire **DefaultInlineConstraintResolver** class by implementing the **IInlineConstraintResolver** interface.</span></span> <span data-ttu-id="637c0-248">Tím nahradí všechny předdefinované omezení, pokud implementace **IInlineConstraintResolver** konkrétně přidá je.</span><span class="sxs-lookup"><span data-stu-id="637c0-248">Doing so will replace all of the built-in constraints, unless your implementation of **IInlineConstraintResolver** specifically adds them.</span></span>

<a id="optional"></a>
## <a name="optional-uri-parameters-and-default-values"></a><span data-ttu-id="637c0-249">Volitelné parametry identifikátoru URI a výchozí hodnoty</span><span class="sxs-lookup"><span data-stu-id="637c0-249">Optional URI Parameters and Default Values</span></span>

<span data-ttu-id="637c0-250">Parametr URI můžete provést jako volitelný přidáním otazníku k parametru trasy.</span><span class="sxs-lookup"><span data-stu-id="637c0-250">You can make a URI parameter optional by adding a question mark to the route parameter.</span></span> <span data-ttu-id="637c0-251">Pokud je parametr trasy volitelný, musíte definovat výchozí hodnotu parametru metody.</span><span class="sxs-lookup"><span data-stu-id="637c0-251">If a route parameter is optional, you must define a default value for the method parameter.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample19.cs)]

<span data-ttu-id="637c0-252">V tomto `/api/books/locale/1033` příkladu a `/api/books/locale` vrátit stejný prostředek.</span><span class="sxs-lookup"><span data-stu-id="637c0-252">In this example, `/api/books/locale/1033` and `/api/books/locale` return the same resource.</span></span>

<span data-ttu-id="637c0-253">Alternativně můžete zadat výchozí hodnotu uvnitř šablony trasy takto:</span><span class="sxs-lookup"><span data-stu-id="637c0-253">Alternatively, you can specify a default value inside the route template, as follows:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample20.cs)]

<span data-ttu-id="637c0-254">To je téměř stejný jako v předchozím příkladu, ale je mírný rozdíl chování při použití výchozí hodnoty.</span><span class="sxs-lookup"><span data-stu-id="637c0-254">This is almost the same as the previous example, but there is a slight difference of behavior when the default value is applied.</span></span>

- <span data-ttu-id="637c0-255">V prvním příkladu ("{lcid:int?}"), výchozí hodnota 1033 je přiřazena přímo parametru metody, takže parametr bude mít tuto přesnou hodnotu.</span><span class="sxs-lookup"><span data-stu-id="637c0-255">In the first example ("{lcid:int?}"), the default value of 1033 is assigned directly to the method parameter, so the parameter will have this exact value.</span></span>
- <span data-ttu-id="637c0-256">V druhém příkladu ("{lcid:int=1033}) prochází výchozí hodnota "1033" procesem vazby modelu.</span><span class="sxs-lookup"><span data-stu-id="637c0-256">In the second example ("{lcid:int=1033}"), the default value of "1033" goes through the model-binding process.</span></span> <span data-ttu-id="637c0-257">Výchozí pořadač modelu převede "1033" na číselnou hodnotu 1033.</span><span class="sxs-lookup"><span data-stu-id="637c0-257">The default model-binder will convert "1033" to the numeric value 1033.</span></span> <span data-ttu-id="637c0-258">Můžete však připojit vlastní pořadač modelu, který by mohl udělat něco jiného.</span><span class="sxs-lookup"><span data-stu-id="637c0-258">However, you could plug in a custom model binder, which might do something different.</span></span>

<span data-ttu-id="637c0-259">(Ve většině případů, pokud nemáte vlastní model pořadače v kanálu, dva formuláře budou ekvivalentní.)</span><span class="sxs-lookup"><span data-stu-id="637c0-259">(In most cases, unless you have custom model binders in your pipeline, the two forms will be equivalent.)</span></span>

<a id="route-names"></a>
## <a name="route-names"></a><span data-ttu-id="637c0-260">Názvy tras</span><span class="sxs-lookup"><span data-stu-id="637c0-260">Route Names</span></span>

<span data-ttu-id="637c0-261">Ve webovém rozhraní API má každá trasa název.</span><span class="sxs-lookup"><span data-stu-id="637c0-261">In Web API, every route has a name.</span></span> <span data-ttu-id="637c0-262">Názvy tras jsou užitečné pro generování propojení, takže můžete zahrnout odkaz do odpovědi HTTP.</span><span class="sxs-lookup"><span data-stu-id="637c0-262">Route names are useful for generating links, so that you can include a link in an HTTP response.</span></span>

<span data-ttu-id="637c0-263">Chcete-li zadat název trasy, nastavte vlastnost **Name** u atributu.</span><span class="sxs-lookup"><span data-stu-id="637c0-263">To specify the route name, set the **Name** property on the attribute.</span></span> <span data-ttu-id="637c0-264">Následující příklad ukazuje, jak nastavit název trasy a také jak použít název trasy při generování propojení.</span><span class="sxs-lookup"><span data-stu-id="637c0-264">The following example shows how to set the route name, and also how to use the route name when generating a link.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample21.cs)]

<a id="order"></a>
## <a name="route-order"></a><span data-ttu-id="637c0-265">Pořadí postupu</span><span class="sxs-lookup"><span data-stu-id="637c0-265">Route Order</span></span>

<span data-ttu-id="637c0-266">Když se rozhraní pokusí porovnat identifikátor URI s postupem, vyhodnotí trasy v určitém pořadí.</span><span class="sxs-lookup"><span data-stu-id="637c0-266">When the framework tries to match a URI with a route, it evaluates the routes in a particular order.</span></span> <span data-ttu-id="637c0-267">Chcete-li zadat pořadí, nastavte vlastnost **Order** v atributu trasy.</span><span class="sxs-lookup"><span data-stu-id="637c0-267">To specify the order, set the **Order** property on the route attribute.</span></span> <span data-ttu-id="637c0-268">Nižší hodnoty jsou vyhodnoceny jako první.</span><span class="sxs-lookup"><span data-stu-id="637c0-268">Lower values are evaluated first.</span></span> <span data-ttu-id="637c0-269">Výchozí hodnota objednávky je nula.</span><span class="sxs-lookup"><span data-stu-id="637c0-269">The default order value is zero.</span></span>

<span data-ttu-id="637c0-270">Zde je, jak je určeno celkové pořadí:</span><span class="sxs-lookup"><span data-stu-id="637c0-270">Here is how the total ordering is determined:</span></span>

1. <span data-ttu-id="637c0-271">Porovnejte **vlastnost Order** atributu route.</span><span class="sxs-lookup"><span data-stu-id="637c0-271">Compare the **Order** property of the route attribute.</span></span>
2. <span data-ttu-id="637c0-272">Podívejte se na každý segment identifikátoru URI v šabloně trasy.</span><span class="sxs-lookup"><span data-stu-id="637c0-272">Look at each URI segment in the route template.</span></span> <span data-ttu-id="637c0-273">Pro každý segment postupujte takto:</span><span class="sxs-lookup"><span data-stu-id="637c0-273">For each segment, order as follows:</span></span>

    1. <span data-ttu-id="637c0-274">Doslovné segmenty.</span><span class="sxs-lookup"><span data-stu-id="637c0-274">Literal segments.</span></span>
    2. <span data-ttu-id="637c0-275">Parametry trasy s omezeními.</span><span class="sxs-lookup"><span data-stu-id="637c0-275">Route parameters with constraints.</span></span>
    3. <span data-ttu-id="637c0-276">Parametry trasy bez omezení.</span><span class="sxs-lookup"><span data-stu-id="637c0-276">Route parameters without constraints.</span></span>
    4. <span data-ttu-id="637c0-277">Segmenty parametrů zástupných symbolů s vazbami.</span><span class="sxs-lookup"><span data-stu-id="637c0-277">Wildcard parameter segments with constraints.</span></span>
    5. <span data-ttu-id="637c0-278">Segmenty parametrů se zástupnými symboly bez omezení.</span><span class="sxs-lookup"><span data-stu-id="637c0-278">Wildcard parameter segments without constraints.</span></span>
3. <span data-ttu-id="637c0-279">V případě nerozhodného spojení jsou trasy seřazeny podle porovnání ordinálních řetězců bez rozlišování velkých a malých písmen ([OrdinalIgnoreCase](https://msdn.microsoft.com/library/system.stringcomparer.ordinalignorecase.aspx)) šablony trasy.</span><span class="sxs-lookup"><span data-stu-id="637c0-279">In the case of a tie, routes are ordered by a case-insensitive ordinal string comparison ([OrdinalIgnoreCase](https://msdn.microsoft.com/library/system.stringcomparer.ordinalignorecase.aspx)) of the route template.</span></span>

<span data-ttu-id="637c0-280">Zde je příklad.</span><span class="sxs-lookup"><span data-stu-id="637c0-280">Here is an example.</span></span> <span data-ttu-id="637c0-281">Předpokládejme, že definujete následující řadič:</span><span class="sxs-lookup"><span data-stu-id="637c0-281">Suppose you define the following controller:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample22.cs)]

<span data-ttu-id="637c0-282">Tyto trasy jsou seřazeny následujícím způsobem.</span><span class="sxs-lookup"><span data-stu-id="637c0-282">These routes are ordered as follows.</span></span>

1. <span data-ttu-id="637c0-283">objednávky/podrobnosti</span><span class="sxs-lookup"><span data-stu-id="637c0-283">orders/details</span></span>
2. <span data-ttu-id="637c0-284">objednávky/{id}</span><span class="sxs-lookup"><span data-stu-id="637c0-284">orders/{id}</span></span>
3. <span data-ttu-id="637c0-285">objednávky/{customerName}</span><span class="sxs-lookup"><span data-stu-id="637c0-285">orders/{customerName}</span></span>
4. <span data-ttu-id="637c0-286">objednávky/{\*datum}</span><span class="sxs-lookup"><span data-stu-id="637c0-286">orders/{\*date}</span></span>
5. <span data-ttu-id="637c0-287">objednávky/nevyřízené</span><span class="sxs-lookup"><span data-stu-id="637c0-287">orders/pending</span></span>

<span data-ttu-id="637c0-288">Všimněte si, že "podrobnosti" je doslovný segment a zobrazí se před "{id}", ale "čekající" se zobrazí jako poslední, protože **Order** vlastnost je 1.</span><span class="sxs-lookup"><span data-stu-id="637c0-288">Notice that "details" is a literal segment and appears before "{id}", but "pending" appears last because the **Order** property is 1.</span></span> <span data-ttu-id="637c0-289">(Tento příklad předpokládá, že neexistují žádní zákazníci s názvem "podrobnosti" nebo "čeká na vyřízení".</span><span class="sxs-lookup"><span data-stu-id="637c0-289">(This example assumes there are no customers named "details" or "pending".</span></span> <span data-ttu-id="637c0-290">Obecně se snažte vyhnout nejednoznačným trasami.</span><span class="sxs-lookup"><span data-stu-id="637c0-290">In general, try to avoid ambiguous routes.</span></span> <span data-ttu-id="637c0-291">V tomto příkladu `GetByCustomer` je lepší šablonou postupu "customers/{customerName}" )</span><span class="sxs-lookup"><span data-stu-id="637c0-291">In this example, a better route template for `GetByCustomer` is "customers/{customerName}" )</span></span>
