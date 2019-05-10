---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-routing-conventions
title: Konvence trasování v rozhraní ASP.NET Web API 2 Odata – ASP.NET 4.x
author: MikeWasson
description: Popisuje konvence trasování, že webové rozhraní API 2 v ASP.NET 4.x používá koncových bodů protokolu OData.
ms.author: riande
ms.date: 07/31/2013
ms.custom: seoapril2019
ms.assetid: adbc175a-14eb-4ab2-a441-d056ffa8266f
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-routing-conventions
msc.type: authoredcontent
ms.openlocfilehash: 63df4a82cd8df92631485b2544117844cfd0ca56
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/06/2019
ms.locfileid: "65130475"
---
# <a name="routing-conventions-in-aspnet-web-api-2-odata"></a>Konvence trasování v rozhraní ASP.NET Web API 2 Odata

podle [Mike Wasson](https://github.com/MikeWasson)

> Tento článek popisuje konvence trasování, že webové rozhraní API 2 v ASP.NET 4.x používá koncových bodů protokolu OData.

Webové rozhraní API získá požadavek OData, mapuje k názvu kontroleru a názvu akce požadavku. Mapování vychází z URI a metodou HTTP. Například `GET /odata/Products(1)` mapuje `ProductsController.GetProduct`.

V části 1 tohoto článku můžu popisují integrované konvencí směrování protokolu OData. Tato konvence jsou navrženy speciálně pro koncových bodů protokolu OData a nahrazují výchozí směrování systém webového rozhraní API. (Nahrazení se stane, když voláte **MapODataRoute**.)

V části 2 můžu ukazují, jak přidat vlastní konvencí směrování. Aktuálně integrované konvence nepokrývají celou oblast prostředí OData pro identifikátory URI, ale můžete rozšířit moct zpracovávat další případy.

- [Integrované konvencí směrování](#conventions)
- [Vlastní konvencí směrování](#custom)

<a id="conventions"></a>
## <a name="built-in-routing-conventions"></a>Integrované konvencí směrování

Než jsem popisují konvencí směrování protokolu OData v rozhraní Web API, je vhodné se seznámit s identifikátory URI protokolu OData. [Identifikátoru URI protokolu OData](http://www.odata.org/documentation/odata-v3-documentation/url-conventions/) se skládá ze:

- Kořenový adresář
- Cesta prostředku
- Možnosti dotazu

![](odata-routing-conventions/_static/image1.png)

Směrování, je důležitou součástí cestu prostředku. Cesta prostředku je rozdělen do segmentů. Například `/Products(1)/Supplier` má tři segmenty:

- `Products` odkazuje na sadu entit s názvem "Produktů".
- `1` je klíč entity, vyberete jednu entitu ze sady.
- `Supplier` je vlastnost navigace, vybere se související entitou.

Proto tato cesta vybere si dodavatele produktu 1.

> [!NOTE]
> Segmenty cesty OData vždy neodpovídají segmentům identifikátoru URI. Například "1" se považuje za segmentu cesty.

**Název kontroleru.** Název kontroleru je vždy odvozen z entity, nastavte v kořenovém adresáři cestu prostředku. Například, pokud je cesta prostředku `/Products(1)/Supplier`, webové rozhraní API hledá kontroler s názvem `ProductsController`.

**Názvy akcí.** Názvy akcí jsou odvozeny z segmenty cesty a modelu entity data model (EDM), jak je uvedeno v následujících tabulkách. V některých případech máte dvě možnosti pro daný název akce. Například "Get" nebo &quot;GetProducts&quot;.

**Dotazování entit**

| Request | Příklad identifikátoru URI | Název akce | Vzorová akce |
| --- | --- | --- | --- |
| ZÍSKAT /entityset | / Produkty | GetEntitySet nebo Get | GetProducts |
| ZÍSKAT /entityset(key) | /Products(1) | GetEntityType nebo Get | GetProduct |
| ZÍSKAT /entityset (klíč) / přetypování | /Products(1)/Models.Book | GetEntityType nebo Get | GetBook |

Další informace najdete v tématu [vytvoření koncového bodu OData jen pro čtení](odata-v3/creating-an-odata-endpoint.md).

**Vytváření, aktualizaci a odstraňování entit**

| Request | Příklad identifikátoru URI | Název akce | Vzorová akce |
| --- | --- | --- | --- |
| Publikovat /entityset | / Produkty | PostEntityType nebo příspěvek | PostProduct |
| Vložit /entityset(key) | /Products(1) | PutEntityType nebo Put | PutProduct |
| Vložit /entityset (klíč) / přetypování | /Products(1)/Models.Book | PutEntityType nebo Put | PutBook |
| Oprava /entityset(key) | /Products(1) | PatchEntityType nebo opravy | PatchProduct |
| Oprava /entityset (klíč) / přetypování | /Products(1)/Models.Book | PatchEntityType nebo opravy | PatchBook |
| DELETE /entityset(key) | /Products(1) | DeleteEntityType nebo Delete | DeleteProduct |
| Odstranit /entityset (klíč) / přetypování | /Products(1)/Models.Book | DeleteEntityType nebo Delete | DeleteBook |

**Navigační vlastnost**

| Request | Příklad identifikátoru URI | Název akce | Vzorová akce |
| --- | --- | --- | --- |
| GET /entityset (klíč) a navigace | / Produkty (1) nebo dodavatele | GetNavigationFromEntityType nebo GetNavigation | GetSupplierFromProduct |
| ZÍSKAT /entityset (klíč) / přetypování/navigace | /Products(1)/Models.Book/Author | GetNavigationFromEntityType nebo GetNavigation | GetAuthorFromBook |

Další informace najdete v tématu [práce se vztahy entit](odata-v3/working-with-entity-relations.md).

**Vytváření a odstraňování propojení**

| Request | Příklad identifikátoru URI | Název akce |
| --- | --- | --- |
| PŘÍSPĚVEK /entityset (klíč) / $links/navigace | /Products(1)/$links/Supplier | CreateLink |
| Vložení /entityset (klíč) / $links/navigace | /Products(1)/$links/Supplier | CreateLink |
| Odstranit /entityset (klíč) / $links/navigace | /Products(1)/$links/Supplier | DeleteLink |
| Odstranit /entityset(key)/$links/navigation(relatedKey) | /Products/(1)/$links/Suppliers(1) | DeleteLink |

Další informace najdete v tématu [práce se vztahy entit](odata-v3/working-with-entity-relations.md).

**Vlastnosti**

*Vyžaduje webového rozhraní API 2*

| Request | Příklad identifikátoru URI | Název akce | Vzorová akce |
| --- | --- | --- | --- |
| GET /entityset (klíč) a vlastnost | / Produkty (1) nebo název | GetPropertyFromEntityType nebo GetProperty | GetNameFromProduct |
| ZÍSKAT /entityset (klíč) / přetypování/vlastnost | /Products(1)/Models.Book/Author | GetPropertyFromEntityType nebo GetProperty | GetTitleFromBook |

**Akce**

| Request | Příklad identifikátoru URI | Název akce | Vzorová akce |
| --- | --- | --- | --- |
| PŘÍSPĚVEK /entityset (klíč) a akce | / Produkty (1) nebo rychlost | ActionNameOnEntityType nebo název akce | RateOnProduct |
| Publikovat /entityset (klíč) / přetypování nebo akce | /Products(1)/Models.Book/CheckOut | ActionNameOnEntityType nebo název akce | CheckOutOnBook |

Další informace najdete v tématu [akcí OData, které](odata-v3/odata-actions.md).

**Podpisy metod**

Tady jsou některá pravidla pro podpisy metod:

- Pokud cesta obsahuje klíč, akce by měl mít parametr s názvem *klíč*.
- Pokud cesta obsahuje klíč do navigační vlastnost, akce by měl mít parametr s názvem *relatedKey*.
- Uspořádání *klíč* a *relatedKey* parametry **[FromODataUri]** parametru.
- POST a PUT požadavky přijmout parametr typu entity.
- Žádosti PATCH potřebují parametr typu **Delta&lt;T&gt;**, kde *T* je typ entity.

Pro referenci tady je příklad, který zobrazuje podpisy metod pro každou integrované konvenci směrování protokolu OData.

[!code-csharp[Main](odata-routing-conventions/samples/sample1.cs)]

<a id="custom"></a>
## <a name="custom-routing-conventions"></a>Vlastní konvencí směrování

Integrované konvence aktuálně nepokrývají všechny možné identifikátorů URI protokolu OData. Můžete přidat nové konvence implementací **IODataRoutingConvention** rozhraní. Toto rozhraní poskytuje dva způsoby:

[!code-csharp[Main](odata-routing-conventions/samples/sample2.cs)]

- **SelectController** vrátí název kontroleru.
- **SelectAction** vrátí název akce.

Pro obě metody Pokud úmluvy se nedá použít u této žádosti, metoda by měla vrátit hodnotu null.

**Objekt ODataPath** parametr představuje cestu k prostředku analyzovanou klauzuli OData. Obsahuje seznam **[ODataPathSegment](https://msdn.microsoft.com/library/system.web.http.odata.routing.odatapathsegment.aspx)** instancí, jeden pro každý segment cesty prostředku. **ODataPathSegment** je abstraktní třída; každý typ segmentu je reprezentován třídou, která je odvozena z **ODataPathSegment**.

**ODataPath.TemplatePath** vlastnosti je řetězec, který představuje zřetězení všechny segmenty cesty. Například, pokud je identifikátor URI `/Products(1)/Supplier`, je šablona cesty &quot;~/entityset/key/navigation&quot;. Všimněte si, že segmenty neodpovídají přímo segmenty identifikátoru URI. Například klíč entity (1) je vyjádřena jako vlastní **ODataPathSegment**.

Obvykle implementace **IODataRoutingConvention** provede následující akce:

1. Porovnejte šablona cesty a zjistěte, jestli tato konvence platí pro aktuální požadavek. Pokud se nevztahuje, vrátí hodnotu null.
2. Pokud platí tato konvence, použijte vlastnosti **ODataPathSegment** instancí k odvození názvu kontroleru a akce.
3. Pro akce přidejte všechny hodnoty do slovníku trasy, která by měla vytvořit vazbu na parametry akce (obvykle klíče entit).

Podívejme se na konkrétní příklad. Integrované konvencí směrování nepodporují indexování do kolekce navigace. Jinými slovy neexistuje žádné vytváření názvů pro identifikátory URI vypadat asi takto:

[!code-javascript[Main](odata-routing-conventions/samples/sample3.js)]

Tady je vlastní konvenci směrování pro zpracování tohoto typu dotazu.

[!code-csharp[Main](odata-routing-conventions/samples/sample4.cs)]

Poznámky:

1. Jsou odvozeny z **EntitySetRoutingConvention**, protože **SelectController** metody v dané třídě je vhodné pro tento nový konvenci směrování. To znamená, že není potřeba znova implementovat **SelectController**.
2. Tato konvence platí pouze pro požadavky GET, a pouze v případě, že je šablona cesty &quot;~/entityset/key/navigation/key&quot;.
3. Je název akce &quot;získat {typ entity EntityType}&quot;, kde *{EntityType}* je typ kolekce navigace. Například &quot;GetSupplier&quot;. Můžete použít libovolné zásady vytváření názvů, který vás zajímá &#8212; právě Ujistěte se, že vaše akce kontroleru odpovídají.
4. Které akce používá dva parametry s názvem *klíč* a *relatedKey*. (Seznam některé názvy předdefinovaných parametrů najdete v tématu [ODataRouteConstants](https://msdn.microsoft.com/library/system.web.http.odata.routing.odatarouteconstants.aspx).)

Dalším krokem je přidání nová konvence do seznamu konvencí směrování. To se stane během konfigurace, jak je znázorněno v následujícím kódu:

[!code-csharp[Main](odata-routing-conventions/samples/sample5.cs)]

Tady jsou některé další ukázky konvencí směrování, která umožňuje zkoumat:

- [CompositeKeyRoutingConvention](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/ODataCompositeKeySample/ODataCompositeKeySample/Extensions/CompositeKeyRoutingConvention.cs)
- [CustomNavigationRoutingConvention](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/ODataServiceSample/ODataService/Extensions/CustomNavigationRoutingConvention.cs)
- [NonBindableActionRoutingConvention](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/ODataActionsSample/ODataActionsSample/NonBindableActionRoutingConvention.cs)
- [ODataVersionRouteConstraint](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/ODataVersioningSample/ODataVersioningSample/Extensions/ODataVersionRouteConstraint.cs)

A samozřejmě samotné rozhraní Web API je open source, abyste si mohli zobrazit [zdrojový kód](http://aspnetwebstack.codeplex.com/) pro integrované konvencí směrování. Ty jsou definovány v **System.Web.Http.OData.Routing.Conventions** oboru názvů.
