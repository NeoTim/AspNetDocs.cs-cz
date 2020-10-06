---
uid: web-api/overview/odata-support-in-aspnet-web-api/supporting-odata-query-options
title: Podpora možností dotazů OData ve webovém rozhraní API ASP.NET 2 – ASP.NET 4. x
author: MikeWasson
description: Přehled s příklady kódu ukazuje podporu možností dotazů OData ve webovém rozhraní API 2 v ASP.NET pro ASP.NET 4. x.
ms.author: riande
ms.date: 02/04/2013
ms.custom: seoapril2019
ms.assetid: 50e6e62b-e72e-4a29-8293-4b67377bd21f
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/supporting-odata-query-options
msc.type: authoredcontent
ms.openlocfilehash: 96820fab7ac89885058962f44ded86cb0184ee97
ms.sourcegitcommit: 4ed0b65ae32d9f35e42ee6296b877747e063df4d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/06/2020
ms.locfileid: "86188613"
---
# <a name="supporting-odata-query-options-in-aspnet-web-api-2"></a><span data-ttu-id="83ed2-103">Podpora možností dotazů OData ve webovém rozhraní API 2 ASP.NET</span><span class="sxs-lookup"><span data-stu-id="83ed2-103">Supporting OData Query Options in ASP.NET Web API 2</span></span>

<span data-ttu-id="83ed2-104">o [Jan Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="83ed2-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="83ed2-105">Tento přehled s příklady kódu ukazuje podporu možností dotazů OData ve webovém rozhraní API 2 v ASP.NET pro ASP.NET 4. x.</span><span class="sxs-lookup"><span data-stu-id="83ed2-105">This overview with code examples demonstrates the supporting OData Query Options in ASP.NET Web API 2 for ASP.NET 4.x.</span></span> 

<span data-ttu-id="83ed2-106">OData definuje parametry, které se dají použít k úpravě dotazu OData.</span><span class="sxs-lookup"><span data-stu-id="83ed2-106">OData defines parameters that can be used to modify an OData query.</span></span> <span data-ttu-id="83ed2-107">Klient odesílá tyto parametry do řetězce dotazu identifikátoru URI požadavku.</span><span class="sxs-lookup"><span data-stu-id="83ed2-107">The client sends these parameters in the query string of the request URI.</span></span> <span data-ttu-id="83ed2-108">Například pro seřazení výsledků klient používá parametr $orderby:</span><span class="sxs-lookup"><span data-stu-id="83ed2-108">For example, to sort the results, a client uses the $orderby parameter:</span></span>

`http://localhost/Products?$orderby=Name`

<span data-ttu-id="83ed2-109">Specifikace OData volá tyto parametry *dotazu*parametrů.</span><span class="sxs-lookup"><span data-stu-id="83ed2-109">The OData specification calls these parameters *query options*.</span></span> <span data-ttu-id="83ed2-110">Můžete povolit možnosti dotazu OData pro libovolný kontroler webového rozhraní API ve vašem projektu &#8212; kontroler nemusí být koncovým bodem OData.</span><span class="sxs-lookup"><span data-stu-id="83ed2-110">You can enable OData query options for any Web API controller in your project &#8212; the controller does not need to be an OData endpoint.</span></span> <span data-ttu-id="83ed2-111">Získáte tak pohodlný způsob, jak přidat funkce, jako je filtrování a řazení, do libovolné aplikace webového rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="83ed2-111">This gives you a convenient way to add features such as filtering and sorting to any Web API application.</span></span>

<span data-ttu-id="83ed2-112">Než povolíte možnosti dotazů, přečtěte si téma [pokyny k zabezpečení OData](odata-security-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="83ed2-112">Before enabling query options, please read the topic [OData Security Guidance](odata-security-guidance.md).</span></span>

- [<span data-ttu-id="83ed2-113">Povolení možností dotazů OData</span><span class="sxs-lookup"><span data-stu-id="83ed2-113">Enabling OData Query Options</span></span>](#enable)
- [<span data-ttu-id="83ed2-114">Příklady dotazů</span><span class="sxs-lookup"><span data-stu-id="83ed2-114">Example Queries</span></span>](#examples)
- [<span data-ttu-id="83ed2-115">Stránkování řízené serverem</span><span class="sxs-lookup"><span data-stu-id="83ed2-115">Server-Driven Paging</span></span>](#server-paging)
- [<span data-ttu-id="83ed2-116">Omezení možností dotazu</span><span class="sxs-lookup"><span data-stu-id="83ed2-116">Limiting the Query Options</span></span>](#limiting_query_options)
- [<span data-ttu-id="83ed2-117">Přímé vyvolání možností dotazu</span><span class="sxs-lookup"><span data-stu-id="83ed2-117">Invoking Query Options Directly</span></span>](#ODataQueryOptions)
- [<span data-ttu-id="83ed2-118">Ověření dotazu</span><span class="sxs-lookup"><span data-stu-id="83ed2-118">Query Validation</span></span>](#query-validation)

<a id="enable"></a>
## <a name="enabling-odata-query-options"></a><span data-ttu-id="83ed2-119">Povolení možností dotazů OData</span><span class="sxs-lookup"><span data-stu-id="83ed2-119">Enabling OData Query Options</span></span>

<span data-ttu-id="83ed2-120">Webové rozhraní API podporuje následující možnosti dotazů OData:</span><span class="sxs-lookup"><span data-stu-id="83ed2-120">Web API supports the following OData query options:</span></span>

| <span data-ttu-id="83ed2-121">Možnost</span><span class="sxs-lookup"><span data-stu-id="83ed2-121">Option</span></span> | <span data-ttu-id="83ed2-122">Popis</span><span class="sxs-lookup"><span data-stu-id="83ed2-122">Description</span></span> |
| --- | --- |
| <span data-ttu-id="83ed2-123">$expand</span><span class="sxs-lookup"><span data-stu-id="83ed2-123">$expand</span></span> | <span data-ttu-id="83ed2-124">Rozšíří vložené přidružené entity.</span><span class="sxs-lookup"><span data-stu-id="83ed2-124">Expands related entities inline.</span></span> |
| <span data-ttu-id="83ed2-125">$filter</span><span class="sxs-lookup"><span data-stu-id="83ed2-125">$filter</span></span> | <span data-ttu-id="83ed2-126">Filtruje výsledky na základě logické podmínky.</span><span class="sxs-lookup"><span data-stu-id="83ed2-126">Filters the results, based on a Boolean condition.</span></span> |
| <span data-ttu-id="83ed2-127">$inlinecount</span><span class="sxs-lookup"><span data-stu-id="83ed2-127">$inlinecount</span></span> | <span data-ttu-id="83ed2-128">Oznamuje serveru, aby zahrnoval celkový počet vyhovujících entit v odpovědi.</span><span class="sxs-lookup"><span data-stu-id="83ed2-128">Tells the server to include the total count of matching entities in the response.</span></span> <span data-ttu-id="83ed2-129">(Hodí se pro stránkování na straně serveru.)</span><span class="sxs-lookup"><span data-stu-id="83ed2-129">(Useful for server-side paging.)</span></span> |
| <span data-ttu-id="83ed2-130">$orderby</span><span class="sxs-lookup"><span data-stu-id="83ed2-130">$orderby</span></span> | <span data-ttu-id="83ed2-131">Seřadí výsledky.</span><span class="sxs-lookup"><span data-stu-id="83ed2-131">Sorts the results.</span></span> |
| <span data-ttu-id="83ed2-132">$select</span><span class="sxs-lookup"><span data-stu-id="83ed2-132">$select</span></span> | <span data-ttu-id="83ed2-133">Vybere vlastnosti, které se mají zahrnout do odpovědi.</span><span class="sxs-lookup"><span data-stu-id="83ed2-133">Selects which properties to include in the response.</span></span> |
| <span data-ttu-id="83ed2-134">$skip</span><span class="sxs-lookup"><span data-stu-id="83ed2-134">$skip</span></span> | <span data-ttu-id="83ed2-135">Přeskočí prvních n výsledků.</span><span class="sxs-lookup"><span data-stu-id="83ed2-135">Skips the first n results.</span></span> |
| <span data-ttu-id="83ed2-136">$top</span><span class="sxs-lookup"><span data-stu-id="83ed2-136">$top</span></span> | <span data-ttu-id="83ed2-137">Vrátí pouze prvních n výsledků.</span><span class="sxs-lookup"><span data-stu-id="83ed2-137">Returns only the first n the results.</span></span> |

<span data-ttu-id="83ed2-138">Chcete-li použít možnosti dotazu OData, je nutné je explicitně povolit.</span><span class="sxs-lookup"><span data-stu-id="83ed2-138">To use OData query options, you must enable them explicitly.</span></span> <span data-ttu-id="83ed2-139">Můžete je povolit globálně pro celou aplikaci nebo je povolit pro konkrétní řadiče nebo konkrétní akce.</span><span class="sxs-lookup"><span data-stu-id="83ed2-139">You can enable them globally for the entire application, or enable them for specific controllers or specific actions.</span></span>

<span data-ttu-id="83ed2-140">Chcete-li povolit možnosti dotazu OData globálně, zavolejte **EnableQuerySupport** na třídu **HttpConfiguration** při spuštění:</span><span class="sxs-lookup"><span data-stu-id="83ed2-140">To enable OData query options globally, call **EnableQuerySupport** on the **HttpConfiguration** class at startup:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample1.cs)]

<span data-ttu-id="83ed2-141">Metoda **EnableQuerySupport** umožňuje globálně použít možnosti dotazu pro všechny akce kontroleru, které vrací typ **IQueryable** .</span><span class="sxs-lookup"><span data-stu-id="83ed2-141">The **EnableQuerySupport** method enables query options globally for any controller action that returns an **IQueryable** type.</span></span> <span data-ttu-id="83ed2-142">Pokud nechcete, aby byly možnosti dotazů povoleny pro celou aplikaci, můžete je povolit pro konkrétní akce kontroleru přidáním atributu **[Queryable]** do metody Action.</span><span class="sxs-lookup"><span data-stu-id="83ed2-142">If you don't want query options enabled for the entire application, you can enable them for specific controller actions by adding the **[Queryable]** attribute to the action method.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample2.cs)]

<a id="examples"></a>
## <a name="example-queries"></a><span data-ttu-id="83ed2-143">Ukázky dotazů</span><span class="sxs-lookup"><span data-stu-id="83ed2-143">Example Queries</span></span>

<span data-ttu-id="83ed2-144">V této části jsou uvedeny typy dotazů, které lze použít v možnostech dotazů OData.</span><span class="sxs-lookup"><span data-stu-id="83ed2-144">This section shows the types of queries that are possible using the OData query options.</span></span> <span data-ttu-id="83ed2-145">Konkrétní podrobnosti o možnostech dotazu najdete v dokumentaci OData na adrese [www.OData.org](http://www.odata.org/).</span><span class="sxs-lookup"><span data-stu-id="83ed2-145">For specific details about the query options, refer to the OData documentation at [www.odata.org](http://www.odata.org/).</span></span>

<span data-ttu-id="83ed2-146">Informace o $expand a $select najdete v tématu [použití $Select, $expand a $value v ASP.NET Web API OData](using-select-expand-and-value.md).</span><span class="sxs-lookup"><span data-stu-id="83ed2-146">For information about $expand and $select, see [Using $select, $expand, and $value in ASP.NET Web API OData](using-select-expand-and-value.md).</span></span>

<span data-ttu-id="83ed2-147">**Stránkování řízené klientem**</span><span class="sxs-lookup"><span data-stu-id="83ed2-147">**Client-Driven Paging**</span></span>

<span data-ttu-id="83ed2-148">U rozsáhlých sad entit může klient chtít omezit počet výsledků.</span><span class="sxs-lookup"><span data-stu-id="83ed2-148">For large entity sets, the client might want to limit the number of results.</span></span> <span data-ttu-id="83ed2-149">Klient může například zobrazit 10 položek najednou a pomocí odkazů Next získat další stránku výsledků.</span><span class="sxs-lookup"><span data-stu-id="83ed2-149">For example, a client might show 10 entries at a time, with "next" links to get the next page of results.</span></span> <span data-ttu-id="83ed2-150">K tomu klient používá $top a $skip možnosti.</span><span class="sxs-lookup"><span data-stu-id="83ed2-150">To do this, the client uses the $top and $skip options.</span></span>

`http://localhost/Products?$top=10&$skip=20`

<span data-ttu-id="83ed2-151">Možnost $top poskytuje maximální počet položek, které se mají vrátit, a možnost $skip vrací počet položek, které se mají přeskočit.</span><span class="sxs-lookup"><span data-stu-id="83ed2-151">The $top option gives the maximum number of entries to return, and the $skip option gives the number of entries to skip.</span></span> <span data-ttu-id="83ed2-152">Předchozí příklad načte položky 21 až 30.</span><span class="sxs-lookup"><span data-stu-id="83ed2-152">The previous example fetches entries 21 through 30.</span></span>

<span data-ttu-id="83ed2-153">**Filtrování**</span><span class="sxs-lookup"><span data-stu-id="83ed2-153">**Filtering**</span></span>

<span data-ttu-id="83ed2-154">Možnost $filter umožňuje klientovi filtrovat výsledky použitím logického výrazu.</span><span class="sxs-lookup"><span data-stu-id="83ed2-154">The $filter option lets a client filter the results by applying a Boolean expression.</span></span> <span data-ttu-id="83ed2-155">Výrazy filtru jsou poměrně výkonné; zahrnují logické a aritmetické operátory, funkce pro řetězce a kalendářní data.</span><span class="sxs-lookup"><span data-stu-id="83ed2-155">The filter expressions are quite powerful; they include logical and arithmetic operators, string functions, and date functions.</span></span>

| <span data-ttu-id="83ed2-156">Vrátí všechny produkty s kategorií rovným "Toys".</span><span class="sxs-lookup"><span data-stu-id="83ed2-156">Return all products with category equal to "Toys".</span></span> | <span data-ttu-id="83ed2-157">`http://localhost/Products?$filter=Category` EQ "Toys"</span><span class="sxs-lookup"><span data-stu-id="83ed2-157">`http://localhost/Products?$filter=Category` eq 'Toys'</span></span> |
| --- | --- |
| <span data-ttu-id="83ed2-158">Vrátí všechny produkty s cenou menší než 10.</span><span class="sxs-lookup"><span data-stu-id="83ed2-158">Return all products with price less than 10.</span></span> | <span data-ttu-id="83ed2-159">`http://localhost/Products?$filter=Price` lt 10</span><span class="sxs-lookup"><span data-stu-id="83ed2-159">`http://localhost/Products?$filter=Price` lt 10</span></span> |
| <span data-ttu-id="83ed2-160">Logické operátory: vrátí všechny produkty, kde Price >= 5 a Price <= 15.</span><span class="sxs-lookup"><span data-stu-id="83ed2-160">Logical operators: Return all products where price >= 5 and price <= 15.</span></span> | <span data-ttu-id="83ed2-161">`http://localhost/Products?$filter=Price` GE 5 a cena Le 15</span><span class="sxs-lookup"><span data-stu-id="83ed2-161">`http://localhost/Products?$filter=Price` ge 5 and Price le 15</span></span> |
| <span data-ttu-id="83ed2-162">Řetězcové funkce: vrátí všechny produkty s "ZZ" v názvu.</span><span class="sxs-lookup"><span data-stu-id="83ed2-162">String functions: Return all products with "zz" in the name.</span></span> | `http://localhost/Products?$filter=substringof('zz',Name)` |
| <span data-ttu-id="83ed2-163">Date Functions: vrátí všechny produkty s ReleaseDate po 2005.</span><span class="sxs-lookup"><span data-stu-id="83ed2-163">Date functions: Return all products with ReleaseDate after 2005.</span></span> | <span data-ttu-id="83ed2-164">`http://localhost/Products?$filter=year(ReleaseDate)` gt 2005</span><span class="sxs-lookup"><span data-stu-id="83ed2-164">`http://localhost/Products?$filter=year(ReleaseDate)` gt 2005</span></span> |

<span data-ttu-id="83ed2-165">**Řazení**</span><span class="sxs-lookup"><span data-stu-id="83ed2-165">**Sorting**</span></span>

<span data-ttu-id="83ed2-166">K seřazení výsledků použijte filtr $orderby.</span><span class="sxs-lookup"><span data-stu-id="83ed2-166">To sort the results, use the $orderby filter.</span></span>

| <span data-ttu-id="83ed2-167">Seřadit podle ceny</span><span class="sxs-lookup"><span data-stu-id="83ed2-167">Sort by price.</span></span> | `http://localhost/Products?$orderby=Price` |
| --- | --- |
| <span data-ttu-id="83ed2-168">Řadit podle ceny v sestupném pořadí (od nejvyšších po nejnižší)</span><span class="sxs-lookup"><span data-stu-id="83ed2-168">Sort by price in descending order (highest to lowest).</span></span> | `http://localhost/Products?$orderby=Price desc` |
| <span data-ttu-id="83ed2-169">Seřadit podle kategorie a pak seřadit podle ceny v sestupném pořadí v rámci kategorií.</span><span class="sxs-lookup"><span data-stu-id="83ed2-169">Sort by category, then sort by price in descending order within categories.</span></span> | `http://localhost/odata/Products?$orderby=Category,Price desc` |

<a id="server-paging"></a>
## <a name="server-driven-paging"></a><span data-ttu-id="83ed2-170">Stránkování řízené serverem</span><span class="sxs-lookup"><span data-stu-id="83ed2-170">Server-Driven Paging</span></span>

<span data-ttu-id="83ed2-171">Pokud vaše databáze obsahuje miliony záznamů, nechcete je posílat všem v jedné datové části.</span><span class="sxs-lookup"><span data-stu-id="83ed2-171">If your database contains millions of records, you don't want to send them all in one payload.</span></span> <span data-ttu-id="83ed2-172">Chcete-li tomu zabránit, může server omezit počet položek, které posílá v rámci jedné odpovědi.</span><span class="sxs-lookup"><span data-stu-id="83ed2-172">To prevent this, the server can limit the number of entries that it sends in a single response.</span></span> <span data-ttu-id="83ed2-173">Pokud chcete povolit stránkování serveru, nastavte vlastnost **PageSize** v atributu **Queryable** .</span><span class="sxs-lookup"><span data-stu-id="83ed2-173">To enable server paging, set the **PageSize** property in the **Queryable** attribute.</span></span> <span data-ttu-id="83ed2-174">Hodnota je maximální počet položek, které se mají vrátit.</span><span class="sxs-lookup"><span data-stu-id="83ed2-174">The value is the maximum number of entries to return.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample3.cs)]

<span data-ttu-id="83ed2-175">Pokud váš kontroler vrátí formát OData, text odpovědi bude obsahovat odkaz na další stránku dat:</span><span class="sxs-lookup"><span data-stu-id="83ed2-175">If your controller returns OData format, the response body will contain a link to the next page of data:</span></span>

[!code-json[Main](supporting-odata-query-options/samples/sample4.json?highlight=8)]

<span data-ttu-id="83ed2-176">Klient může použít tento odkaz k načtení další stránky.</span><span class="sxs-lookup"><span data-stu-id="83ed2-176">The client can use this link to fetch the next page.</span></span> <span data-ttu-id="83ed2-177">Chcete-li zjistit celkový počet položek v sadě výsledků, může klient nastavit možnost dotazu $inlinecount s hodnotou "AllPages".</span><span class="sxs-lookup"><span data-stu-id="83ed2-177">To learn the total number of entries in the result set, the client can set the $inlinecount query option with the value "allpages".</span></span>

`http://localhost/Products?$inlinecount=allpages`

<span data-ttu-id="83ed2-178">Hodnota "AllPages" oznamuje serveru, aby obsahoval celkový počet v odpovědi:</span><span class="sxs-lookup"><span data-stu-id="83ed2-178">The value "allpages" tells the server to include the total count in the response:</span></span>

[!code-json[Main](supporting-odata-query-options/samples/sample5.json?highlight=3)]

> [!NOTE]
> <span data-ttu-id="83ed2-179">Odkazy na další stránku a vložený počet vyžadují formát OData.</span><span class="sxs-lookup"><span data-stu-id="83ed2-179">Next-page links and inline count both require OData format.</span></span> <span data-ttu-id="83ed2-180">Důvodem je, že OData definuje speciální pole v těle odpovědi, aby obsahovala odkaz a počet.</span><span class="sxs-lookup"><span data-stu-id="83ed2-180">The reason is that OData defines special fields in the response body to hold the link and count.</span></span>

<span data-ttu-id="83ed2-181">Pro formáty jiné než OData je stále možné podporovat odkazy na další stránky a vložený počet tím, že se výsledky dotazu zabalí do objektu \*\*PageResult &lt; T &gt; \*\* .</span><span class="sxs-lookup"><span data-stu-id="83ed2-181">For non-OData formats, it is still possible to support next-page links and inline count, by wrapping the query results in a **PageResult&lt;T&gt;** object.</span></span> <span data-ttu-id="83ed2-182">Vyžaduje ale trochu více kódu.</span><span class="sxs-lookup"><span data-stu-id="83ed2-182">However, it requires a bit more code.</span></span> <span data-ttu-id="83ed2-183">Tady je příklad:</span><span class="sxs-lookup"><span data-stu-id="83ed2-183">Here is an example:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample6.cs)]

<span data-ttu-id="83ed2-184">Tady je příklad odpovědi JSON:</span><span class="sxs-lookup"><span data-stu-id="83ed2-184">Here is an example JSON response:</span></span>

[!code-json[Main](supporting-odata-query-options/samples/sample7.json)]

<a id="limiting_query_options"></a>
## <a name="limiting-the-query-options"></a><span data-ttu-id="83ed2-185">Omezení možností dotazu</span><span class="sxs-lookup"><span data-stu-id="83ed2-185">Limiting the Query Options</span></span>

<span data-ttu-id="83ed2-186">Možnosti dotazu umožňují klientovi velkou kontrolu nad dotazem, který je spuštěn na serveru.</span><span class="sxs-lookup"><span data-stu-id="83ed2-186">The query options give the client a lot of control over the query that is run on the server.</span></span> <span data-ttu-id="83ed2-187">V některých případech můžete chtít omezit dostupné možnosti z hlediska zabezpečení nebo výkonu.</span><span class="sxs-lookup"><span data-stu-id="83ed2-187">In some cases, you might want to limit the available options for security or performance reasons.</span></span> <span data-ttu-id="83ed2-188">Atribut **[Queryable]** obsahuje některé předdefinované vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="83ed2-188">The **[Queryable]** attribute has some built in properties for this.</span></span> <span data-ttu-id="83ed2-189">Tady je několik příkladů.</span><span class="sxs-lookup"><span data-stu-id="83ed2-189">Here are some examples.</span></span>

<span data-ttu-id="83ed2-190">Povolí pouze $skip a $top, aby podporovaly stránkování a nic jiného:</span><span class="sxs-lookup"><span data-stu-id="83ed2-190">Allow only $skip and $top, to support paging and nothing else:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample8.cs)]

<span data-ttu-id="83ed2-191">Povoluje řazení pouze pomocí určitých vlastností, aby nedocházelo k řazení vlastností, které nejsou indexovány v databázi:</span><span class="sxs-lookup"><span data-stu-id="83ed2-191">Allow ordering only by certain properties, to prevent sorting on properties that are not indexed in the database:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample9.cs)]

<span data-ttu-id="83ed2-192">Povolí logickou funkci EQ, ale žádné jiné logické funkce:</span><span class="sxs-lookup"><span data-stu-id="83ed2-192">Allow the "eq" logical function but no other logical functions:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample10.cs)]

<span data-ttu-id="83ed2-193">Nepovolujte žádné aritmetické operátory:</span><span class="sxs-lookup"><span data-stu-id="83ed2-193">Do not allow any arithmetic operators:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample11.cs)]

<span data-ttu-id="83ed2-194">Možnosti lze omezit globálně vytvořením instance **QueryableAttribute** a jejím předáním funkci **EnableQuerySupport** :</span><span class="sxs-lookup"><span data-stu-id="83ed2-194">You can restrict options globally by constructing a **QueryableAttribute** instance and passing it to the **EnableQuerySupport** function:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample12.cs)]

<a id="ODataQueryOptions"></a>
## <a name="invoking-query-options-directly"></a><span data-ttu-id="83ed2-195">Přímé vyvolání možností dotazu</span><span class="sxs-lookup"><span data-stu-id="83ed2-195">Invoking Query Options Directly</span></span>

<span data-ttu-id="83ed2-196">Namísto použití atributu **[Queryable]** lze vyvolat možnosti dotazu přímo v řadiči.</span><span class="sxs-lookup"><span data-stu-id="83ed2-196">Instead of using the **[Queryable]** attribute, you can invoke the query options directly in your controller.</span></span> <span data-ttu-id="83ed2-197">Uděláte to tak, že do metody kontroleru přidáte parametr **ODataQueryOptions** .</span><span class="sxs-lookup"><span data-stu-id="83ed2-197">To do so, add an **ODataQueryOptions** parameter to the controller method.</span></span> <span data-ttu-id="83ed2-198">V takovém případě nepotřebujete atribut **[Queryable]** .</span><span class="sxs-lookup"><span data-stu-id="83ed2-198">In this case, you don't need the **[Queryable]** attribute.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample13.cs)]

<span data-ttu-id="83ed2-199">Webové rozhraní API naplní **ODataQueryOptions** z řetězce dotazu identifikátoru URI.</span><span class="sxs-lookup"><span data-stu-id="83ed2-199">Web API populates the **ODataQueryOptions** from the URI query string.</span></span> <span data-ttu-id="83ed2-200">Chcete-li použít dotaz, předejte rozhraní **IQueryable** do metody **ApplyTo** .</span><span class="sxs-lookup"><span data-stu-id="83ed2-200">To apply the query, pass an **IQueryable** to the **ApplyTo** method.</span></span> <span data-ttu-id="83ed2-201">Metoda vrátí jinou metodu **IQueryable**.</span><span class="sxs-lookup"><span data-stu-id="83ed2-201">The method returns another **IQueryable**.</span></span>

<span data-ttu-id="83ed2-202">V případě pokročilých scénářů, pokud nemáte poskytovatele dotazů **IQueryable** , můžete prozkoumávat **ODataQueryOptions** a překládat možnosti dotazu do jiného formuláře.</span><span class="sxs-lookup"><span data-stu-id="83ed2-202">For advanced scenarios, if you do not have an **IQueryable** query provider, you can examine the **ODataQueryOptions** and translate the query options into another form.</span></span> <span data-ttu-id="83ed2-203">(Příklad: viz Blogový příspěvek RaghuRam Nadiminti [překladu dotazů OData na HQL](https://blogs.msdn.com/b/webdev/archive/2013/02/25/translating-odata-queries-to-hql.aspx), který obsahuje také [ukázku](http://aspnet.codeplex.com/SourceControl/changeset/view/75a56ec99968#Samples/WebApi/NHibernateQueryableSample/Readme.txt).)</span><span class="sxs-lookup"><span data-stu-id="83ed2-203">(For example, see RaghuRam Nadiminti's blog post [Translating OData queries to HQL](https://blogs.msdn.com/b/webdev/archive/2013/02/25/translating-odata-queries-to-hql.aspx), which also includes a [sample](http://aspnet.codeplex.com/SourceControl/changeset/view/75a56ec99968#Samples/WebApi/NHibernateQueryableSample/Readme.txt).)</span></span>

<a id="query-validation"></a>
## <a name="query-validation"></a><span data-ttu-id="83ed2-204">Ověření dotazu</span><span class="sxs-lookup"><span data-stu-id="83ed2-204">Query Validation</span></span>

<span data-ttu-id="83ed2-205">Atribut **[Queryable]** ověřuje dotaz před jeho provedením.</span><span class="sxs-lookup"><span data-stu-id="83ed2-205">The **[Queryable]** attribute validates the query before executing it.</span></span> <span data-ttu-id="83ed2-206">Krok ověřování se provádí v metodě **QueryableAttribute. ValidateQuery** .</span><span class="sxs-lookup"><span data-stu-id="83ed2-206">The validation step is performed in the **QueryableAttribute.ValidateQuery** method.</span></span> <span data-ttu-id="83ed2-207">Můžete také přizpůsobit proces ověřování.</span><span class="sxs-lookup"><span data-stu-id="83ed2-207">You can also customize the validation process.</span></span>

<span data-ttu-id="83ed2-208">Viz také [Průvodce zabezpečením OData](odata-security-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="83ed2-208">Also see [OData Security Guidance](odata-security-guidance.md).</span></span>

<span data-ttu-id="83ed2-209">Nejprve přepište jednu z tříd validátoru, která je definována v oboru názvů **Web. http. OData. Query. validátors** .</span><span class="sxs-lookup"><span data-stu-id="83ed2-209">First, override one of the validator classes that is defined in the **Web.Http.OData.Query.Validators** namespace.</span></span> <span data-ttu-id="83ed2-210">Například následující třída validátoru zakáže možnost ' DESC ' pro možnost $orderby.</span><span class="sxs-lookup"><span data-stu-id="83ed2-210">For example, the following validator class disables the 'desc' option for the $orderby option.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample14.cs)]

<span data-ttu-id="83ed2-211">Podtříd atributu **[Queryable]** pro přepsání metody **ValidateQuery** .</span><span class="sxs-lookup"><span data-stu-id="83ed2-211">Subclass the **[Queryable]** attribute to override the **ValidateQuery** method.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample15.cs)]

<span data-ttu-id="83ed2-212">Pak vlastní atribut nastavte buď globálně, nebo podle kontroleru:</span><span class="sxs-lookup"><span data-stu-id="83ed2-212">Then set your custom attribute either globally or per-controller:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample16.cs)]

<span data-ttu-id="83ed2-213">Pokud používáte **ODataQueryOptions** přímo, nastavte ověřovací modul na možnosti:</span><span class="sxs-lookup"><span data-stu-id="83ed2-213">If you are using **ODataQueryOptions** directly, set the validator on the options:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample17.cs)]
