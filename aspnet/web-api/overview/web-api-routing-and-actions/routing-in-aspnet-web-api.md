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
# <a name="routing-in-aspnet-web-api"></a>Směrování v ASP.NET webovérozhraní API

podle [Mike Wasson](https://github.com/MikeWasson)

Tento článek popisuje, jak ASP.NET webové rozhraní API směruje požadavky HTTP na řadiče.

> [!NOTE]
> Pokud jste obeznámeni s ASP.NET MVC, směrování webového rozhraní API je velmi podobný směrování MVC. Hlavní rozdíl spočá, že webové rozhraní API používá k výběru akce sloveso HTTP, nikoli cestu IDENTIFIKÁTORURI. Můžete také použít směrování ve stylu MVC ve webovém rozhraní API. Tento článek nepředpokládá žádné znalosti ASP.NET MVC.

## <a name="routing-tables"></a>Směrování tabulek

V ASP.NET webové rozhraní API je *řadič* třídou, která zpracovává požadavky HTTP. Veřejné metody regulátoru se nazývají *akční metody* nebo jednoduše *akce*. Když rozhraní webového rozhraní API obdrží požadavek, směruje požadavek na akci.

Chcete-li zjistit, kterou akci vyvolat, rozhraní používá *směrovací tabulku*. Šablona projektu Visual Studia pro webové rozhraní API vytvoří výchozí trasu:

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample1.cs)]

Tato trasa je definována v *souboru WebApiConfig.cs,* který je umístěn v adresáři *Start\_aplikace:*

![](routing-in-aspnet-web-api/_static/image1.png)

Další informace o `WebApiConfig` třídě naleznete v [tématu Configuring ASP.NET Web API](../advanced/configuring-aspnet-web-api.md).

Pokud vlastní webapi, musíte nastavit směrovací tabulku `HttpSelfHostConfiguration` přímo na objektu. Další informace naleznete [v tématu Self-Host a Web API](../older-versions/self-host-a-web-api.md).

Každá položka ve směrovací tabulce obsahuje *šablonu postupu*. Výchozí šablona trasy pro &quot;webové rozhraní API je api/{controller}/{id}&quot;. V této &quot;šabloně je rozhraní API&quot; segmentem cesty literálu a {controller} a {id} jsou zástupné proměnné.

Když rozhraní webového rozhraní API obdrží požadavek HTTP, pokusí se porovnat identifikátor URI s jednou ze šablon tras ve směrovací tabulce. Pokud se neshoduje žádná trasa, klient obdrží chybu 404. Například následující identifikátory URI odpovídají výchozí trase:

- /api/kontakty
- /api/kontakty/1
- /api/products/gizmo1

Následující identifikátor URI se však neshoduje, &quot;&quot; protože postrádá segment rozhraní API:

- /kontakty/1

> [!NOTE]
> Důvodem pro použití "api" v trase je, aby se zabránilo kolizím s ASP.NET směrování MVC. Tímto způsobem můžete &quot;mít&quot; /kontakty přejít na &quot;řadič MVC a /api/contacts&quot; přejít na řadič webového rozhraní API. Samozřejmě, pokud se vám nelíbí tato konvence, můžete změnit výchozí směrovací tabulku.

Jakmile je nalezena odpovídající trasa, webové rozhraní API vybere řadič a akci:

- Chcete-li najít řadič, &quot;&quot; webové rozhraní API přidá řadič k hodnotě proměnné *{controller}.*
- Chcete-li najít akci, webové rozhraní API se podívá na sloveso HTTP a pak vyhledá akci, jejíž název začíná tímto názvem slovesa HTTP. Například s požadavkem GET webové rozhraní API &quot;hledá&quot;akci &quot;s&quot; předponou Get , například GetContact nebo &quot;GetAllContacts&quot;. Tato konvence se vztahuje pouze na get, post, put, delete, head, options a patch slovesa. Ostatní slovesa PROTOKOLU HTTP můžete povolit pomocí atributů na řadiči. Příklad uvidíme později.
- Ostatní zástupné proměnné v šabloně trasy, například *{id},* jsou mapovány na parametry akce.

Pojďme se podívat na příklad. Předpokládejme, že definujete následující řadič:

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample2.cs)]

Zde jsou některé možné požadavky HTTP, spolu s akcí, která se vyvolá pro každý:

| Sloveso HTTP | Cesta identifikátoru URI | Akce | Parametr |
| --- | --- | --- | --- |
| GET | api/produkty | GetAllProducts | *(žádný)* |
| GET | api/produkty/4 | GetProductById | 4 |
| DELETE | api/produkty/4 | Odstranit produkt | 4 |
| POST | api/produkty | *(bez shody)* |  |

Všimněte si, že segment *{id}* identifikátoru URI, pokud je přítomen, je mapován na parametr *id* akce. V tomto příkladu řadič definuje dvě metody GET, jednu s parametrem *id* a jednu bez parametrů.

Všimněte si také, že požadavek POST se &quot;nezdaří, protože řadič nedefinuje Post... &quot; metodou.

## <a name="routing-variations"></a>Varianty směrování

Předchozí část popisuje základní mechanismus směrování pro ASP.NET webové rozhraní API. Tato část popisuje některé varianty.

### <a name="http-verbs"></a>Http slovesa

Namísto použití konvence pojmenování pro slovesa HTTP můžete explicitně zadat sloveso HTTP pro akci zdobením metody akce jedním z následujících atributů:

- `[HttpGet]`
- `[HttpPut]`
- `[HttpPost]`
- `[HttpDelete]`
- `[HttpHead]`
- `[HttpOptions]`
- `[HttpPatch]`

V následujícím příkladu `FindProduct` je metoda mapována na požadavky GET:

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample3.cs)]

Chcete-li povolit více sloves protokolu HTTP pro akci nebo povolit slovesa HTTP jiná než `[AcceptVerbs]` GET, PUT, POST, DELETE, HEAD, OPTIONS a PATCH, použijte atribut, který přebírá seznam sloves PROTOKOLU HTTP.

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample4.cs)]

<a id="routing_by_action_name"></a>
### <a name="routing-by-action-name"></a>Směrování podle názvu akce

S výchozí šablonou směrování používá webové rozhraní API k výběru akce sloveso HTTP. Můžete však také vytvořit trasu, kde je název akce zahrnut v identifikátoru URI:

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample5.cs)]

V této šabloně trasy pojmenuje parametr *{action}* metodu akce na řadiči. Pomocí tohoto stylu směrování použijte atributy k určení povolených sloves PROTOKOLU HTTP. Předpokládejme například, že váš řadič má následující metodu:

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample6.cs)]

V tomto případě get požadavek na "api/products/details/1" by mapovat na metodu. `Details` Tento styl směrování je podobný ASP.NET MVC a může být vhodný pro rozhraní API ve stylu RPC.

Název akce můžete přepsat pomocí `[ActionName]` atributu. V následujícím příkladu jsou dvě akce, které mapují na &quot;api/products/thumbnail/*id*. Jeden podporuje GET a druhý podporuje POST:

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample7.cs)]

### <a name="non-actions"></a>Neakce

Chcete-li zabránit vyvolání metody jako akce, použijte `[NonAction]` atribut. To signalizuje rámci, že metoda není akce, i v případě, že by jinak odpovídat pravidla směrování.

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample8.cs)]

## <a name="further-reading"></a>Další čtení

Toto téma poskytlo zobrazení směrování na vysoké úrovni. Další podrobnosti naleznete v [tématu Směrování a výběr akce](routing-and-action-selection.md), který přesně popisuje, jak rozhraní odpovídá uri na trasu, vybere řadič a potom vybere akci vyvolat.
