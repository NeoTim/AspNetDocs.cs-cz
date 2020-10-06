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
# <a name="supporting-odata-query-options-in-aspnet-web-api-2"></a>Podpora možností dotazů OData ve webovém rozhraní API 2 ASP.NET

o [Jan Wasson](https://github.com/MikeWasson)

Tento přehled s příklady kódu ukazuje podporu možností dotazů OData ve webovém rozhraní API 2 v ASP.NET pro ASP.NET 4. x. 

OData definuje parametry, které se dají použít k úpravě dotazu OData. Klient odesílá tyto parametry do řetězce dotazu identifikátoru URI požadavku. Například pro seřazení výsledků klient používá parametr $orderby:

`http://localhost/Products?$orderby=Name`

Specifikace OData volá tyto parametry *dotazu*parametrů. Můžete povolit možnosti dotazu OData pro libovolný kontroler webového rozhraní API ve vašem projektu &#8212; kontroler nemusí být koncovým bodem OData. Získáte tak pohodlný způsob, jak přidat funkce, jako je filtrování a řazení, do libovolné aplikace webového rozhraní API.

Než povolíte možnosti dotazů, přečtěte si téma [pokyny k zabezpečení OData](odata-security-guidance.md).

- [Povolení možností dotazů OData](#enable)
- [Příklady dotazů](#examples)
- [Stránkování řízené serverem](#server-paging)
- [Omezení možností dotazu](#limiting_query_options)
- [Přímé vyvolání možností dotazu](#ODataQueryOptions)
- [Ověření dotazu](#query-validation)

<a id="enable"></a>
## <a name="enabling-odata-query-options"></a>Povolení možností dotazů OData

Webové rozhraní API podporuje následující možnosti dotazů OData:

| Možnost | Popis |
| --- | --- |
| $expand | Rozšíří vložené přidružené entity. |
| $filter | Filtruje výsledky na základě logické podmínky. |
| $inlinecount | Oznamuje serveru, aby zahrnoval celkový počet vyhovujících entit v odpovědi. (Hodí se pro stránkování na straně serveru.) |
| $orderby | Seřadí výsledky. |
| $select | Vybere vlastnosti, které se mají zahrnout do odpovědi. |
| $skip | Přeskočí prvních n výsledků. |
| $top | Vrátí pouze prvních n výsledků. |

Chcete-li použít možnosti dotazu OData, je nutné je explicitně povolit. Můžete je povolit globálně pro celou aplikaci nebo je povolit pro konkrétní řadiče nebo konkrétní akce.

Chcete-li povolit možnosti dotazu OData globálně, zavolejte **EnableQuerySupport** na třídu **HttpConfiguration** při spuštění:

[!code-csharp[Main](supporting-odata-query-options/samples/sample1.cs)]

Metoda **EnableQuerySupport** umožňuje globálně použít možnosti dotazu pro všechny akce kontroleru, které vrací typ **IQueryable** . Pokud nechcete, aby byly možnosti dotazů povoleny pro celou aplikaci, můžete je povolit pro konkrétní akce kontroleru přidáním atributu **[Queryable]** do metody Action.

[!code-csharp[Main](supporting-odata-query-options/samples/sample2.cs)]

<a id="examples"></a>
## <a name="example-queries"></a>Ukázky dotazů

V této části jsou uvedeny typy dotazů, které lze použít v možnostech dotazů OData. Konkrétní podrobnosti o možnostech dotazu najdete v dokumentaci OData na adrese [www.OData.org](http://www.odata.org/).

Informace o $expand a $select najdete v tématu [použití $Select, $expand a $value v ASP.NET Web API OData](using-select-expand-and-value.md).

**Stránkování řízené klientem**

U rozsáhlých sad entit může klient chtít omezit počet výsledků. Klient může například zobrazit 10 položek najednou a pomocí odkazů Next získat další stránku výsledků. K tomu klient používá $top a $skip možnosti.

`http://localhost/Products?$top=10&$skip=20`

Možnost $top poskytuje maximální počet položek, které se mají vrátit, a možnost $skip vrací počet položek, které se mají přeskočit. Předchozí příklad načte položky 21 až 30.

**Filtrování**

Možnost $filter umožňuje klientovi filtrovat výsledky použitím logického výrazu. Výrazy filtru jsou poměrně výkonné; zahrnují logické a aritmetické operátory, funkce pro řetězce a kalendářní data.

| Vrátí všechny produkty s kategorií rovným "Toys". | `http://localhost/Products?$filter=Category` EQ "Toys" |
| --- | --- |
| Vrátí všechny produkty s cenou menší než 10. | `http://localhost/Products?$filter=Price` lt 10 |
| Logické operátory: vrátí všechny produkty, kde Price >= 5 a Price <= 15. | `http://localhost/Products?$filter=Price` GE 5 a cena Le 15 |
| Řetězcové funkce: vrátí všechny produkty s "ZZ" v názvu. | `http://localhost/Products?$filter=substringof('zz',Name)` |
| Date Functions: vrátí všechny produkty s ReleaseDate po 2005. | `http://localhost/Products?$filter=year(ReleaseDate)` gt 2005 |

**Řazení**

K seřazení výsledků použijte filtr $orderby.

| Seřadit podle ceny | `http://localhost/Products?$orderby=Price` |
| --- | --- |
| Řadit podle ceny v sestupném pořadí (od nejvyšších po nejnižší) | `http://localhost/Products?$orderby=Price desc` |
| Seřadit podle kategorie a pak seřadit podle ceny v sestupném pořadí v rámci kategorií. | `http://localhost/odata/Products?$orderby=Category,Price desc` |

<a id="server-paging"></a>
## <a name="server-driven-paging"></a>Stránkování řízené serverem

Pokud vaše databáze obsahuje miliony záznamů, nechcete je posílat všem v jedné datové části. Chcete-li tomu zabránit, může server omezit počet položek, které posílá v rámci jedné odpovědi. Pokud chcete povolit stránkování serveru, nastavte vlastnost **PageSize** v atributu **Queryable** . Hodnota je maximální počet položek, které se mají vrátit.

[!code-csharp[Main](supporting-odata-query-options/samples/sample3.cs)]

Pokud váš kontroler vrátí formát OData, text odpovědi bude obsahovat odkaz na další stránku dat:

[!code-json[Main](supporting-odata-query-options/samples/sample4.json?highlight=8)]

Klient může použít tento odkaz k načtení další stránky. Chcete-li zjistit celkový počet položek v sadě výsledků, může klient nastavit možnost dotazu $inlinecount s hodnotou "AllPages".

`http://localhost/Products?$inlinecount=allpages`

Hodnota "AllPages" oznamuje serveru, aby obsahoval celkový počet v odpovědi:

[!code-json[Main](supporting-odata-query-options/samples/sample5.json?highlight=3)]

> [!NOTE]
> Odkazy na další stránku a vložený počet vyžadují formát OData. Důvodem je, že OData definuje speciální pole v těle odpovědi, aby obsahovala odkaz a počet.

Pro formáty jiné než OData je stále možné podporovat odkazy na další stránky a vložený počet tím, že se výsledky dotazu zabalí do objektu **PageResult &lt; T &gt; ** . Vyžaduje ale trochu více kódu. Tady je příklad:

[!code-csharp[Main](supporting-odata-query-options/samples/sample6.cs)]

Tady je příklad odpovědi JSON:

[!code-json[Main](supporting-odata-query-options/samples/sample7.json)]

<a id="limiting_query_options"></a>
## <a name="limiting-the-query-options"></a>Omezení možností dotazu

Možnosti dotazu umožňují klientovi velkou kontrolu nad dotazem, který je spuštěn na serveru. V některých případech můžete chtít omezit dostupné možnosti z hlediska zabezpečení nebo výkonu. Atribut **[Queryable]** obsahuje některé předdefinované vlastnosti. Tady je několik příkladů.

Povolí pouze $skip a $top, aby podporovaly stránkování a nic jiného:

[!code-csharp[Main](supporting-odata-query-options/samples/sample8.cs)]

Povoluje řazení pouze pomocí určitých vlastností, aby nedocházelo k řazení vlastností, které nejsou indexovány v databázi:

[!code-csharp[Main](supporting-odata-query-options/samples/sample9.cs)]

Povolí logickou funkci EQ, ale žádné jiné logické funkce:

[!code-csharp[Main](supporting-odata-query-options/samples/sample10.cs)]

Nepovolujte žádné aritmetické operátory:

[!code-csharp[Main](supporting-odata-query-options/samples/sample11.cs)]

Možnosti lze omezit globálně vytvořením instance **QueryableAttribute** a jejím předáním funkci **EnableQuerySupport** :

[!code-csharp[Main](supporting-odata-query-options/samples/sample12.cs)]

<a id="ODataQueryOptions"></a>
## <a name="invoking-query-options-directly"></a>Přímé vyvolání možností dotazu

Namísto použití atributu **[Queryable]** lze vyvolat možnosti dotazu přímo v řadiči. Uděláte to tak, že do metody kontroleru přidáte parametr **ODataQueryOptions** . V takovém případě nepotřebujete atribut **[Queryable]** .

[!code-csharp[Main](supporting-odata-query-options/samples/sample13.cs)]

Webové rozhraní API naplní **ODataQueryOptions** z řetězce dotazu identifikátoru URI. Chcete-li použít dotaz, předejte rozhraní **IQueryable** do metody **ApplyTo** . Metoda vrátí jinou metodu **IQueryable**.

V případě pokročilých scénářů, pokud nemáte poskytovatele dotazů **IQueryable** , můžete prozkoumávat **ODataQueryOptions** a překládat možnosti dotazu do jiného formuláře. (Příklad: viz Blogový příspěvek RaghuRam Nadiminti [překladu dotazů OData na HQL](https://blogs.msdn.com/b/webdev/archive/2013/02/25/translating-odata-queries-to-hql.aspx), který obsahuje také [ukázku](http://aspnet.codeplex.com/SourceControl/changeset/view/75a56ec99968#Samples/WebApi/NHibernateQueryableSample/Readme.txt).)

<a id="query-validation"></a>
## <a name="query-validation"></a>Ověření dotazu

Atribut **[Queryable]** ověřuje dotaz před jeho provedením. Krok ověřování se provádí v metodě **QueryableAttribute. ValidateQuery** . Můžete také přizpůsobit proces ověřování.

Viz také [Průvodce zabezpečením OData](odata-security-guidance.md).

Nejprve přepište jednu z tříd validátoru, která je definována v oboru názvů **Web. http. OData. Query. validátors** . Například následující třída validátoru zakáže možnost ' DESC ' pro možnost $orderby.

[!code-csharp[Main](supporting-odata-query-options/samples/sample14.cs)]

Podtříd atributu **[Queryable]** pro přepsání metody **ValidateQuery** .

[!code-csharp[Main](supporting-odata-query-options/samples/sample15.cs)]

Pak vlastní atribut nastavte buď globálně, nebo podle kontroleru:

[!code-csharp[Main](supporting-odata-query-options/samples/sample16.cs)]

Pokud používáte **ODataQueryOptions** přímo, nastavte ověřovací modul na možnosti:

[!code-csharp[Main](supporting-odata-query-options/samples/sample17.cs)]
