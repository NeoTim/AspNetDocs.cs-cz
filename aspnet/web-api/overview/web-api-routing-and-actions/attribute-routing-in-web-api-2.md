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
# <a name="attribute-routing-in-aspnet-web-api-2"></a>Směrování atributů v ASP.NET webovérozhraní API 2

podle [Mike Wasson](https://github.com/MikeWasson)

*Směrování* je způsob, jakým webové rozhraní API odpovídá identifikátoru URI akci. Webové rozhraní API 2 podporuje nový typ směrování, nazývaný *směrování atributů*. Jak název napovídá, směrování atributů používá k definování tras atributy. Směrování atributů poskytuje větší kontrolu nad identifikátory URI ve webovém rozhraní API. Můžete například snadno vytvořit identifikátory URI, které popisují hierarchie prostředků.

Dřívější styl směrování, nazývaný směrování založený na konvencích, je stále plně podporován. Ve skutečnosti můžete kombinovat obě techniky ve stejném projektu.

Toto téma ukazuje, jak povolit směrování atributů a popisuje různé možnosti směrování atributů. Kurz na konci výuky, která používá směrování atributů, najdete [v tématu Vytvoření rozhraní REST API s směrováním atributů ve webovém rozhraní API 2](create-a-rest-api-with-attribute-routing.md).

## <a name="prerequisites"></a>Požadavky

[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Verze Společenství, Professional nebo Enterprise

Případně použijte NuGet Správce balíčků k instalaci potřebných balíčků. V nabídce **Nástroje** v sadě Visual Studio vyberte **Položku Správce balíčků NuGet**a potom vyberte **konzolu správce balíčků**. V okně Konzoly správce balíčků zadejte následující příkaz:

`Install-Package Microsoft.AspNet.WebApi.WebHost`

<a id="why"></a>
## <a name="why-attribute-routing"></a>Proč směrování atributů?

První vydání webového rozhraní API používá směrování *založené na konvencích.* V tomto typu směrování definujete jednu nebo více šablon tras, které jsou v podstatě parametrizované řetězce. Když rozhraní obdrží požadavek, odpovídá identifikátoru URI proti šabloně trasy. Další informace o směrování založeném na konvencích naleznete [v tématu Směrování v ASP.NET webovérozhraní API](routing-in-aspnet-web-api.md).

Jednou z výhod směrování na základě konvence je, že šablony jsou definovány na jednom místě a pravidla směrování jsou použity konzistentně ve všech řadičích. Bohužel směrování založené na konvencích ztěžuje podporu určitých vzorů URI, které jsou běžné v restful api. Například zdroje často obsahují podřízené prostředky: Zákazníci mají objednávky, filmy mají herce, knihy mají autory a tak dále. Je přirozené vytvářet identifikátory URI, které odrážejí tyto vztahy:

`/customers/1/orders`

Tento typ identifikátoru URI je obtížné vytvořit pomocí směrování založeného na konvencích. I když to lze provést, výsledky nejsou škálovat dobře, pokud máte mnoho řadičů nebo typů prostředků.

Při směrování atributů je triviální definovat trasu pro tento identifikátor URI. Jednoduše přidáte atribut do akce kontroleru:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample1.cs)]

Zde jsou některé další vzory, které atribut směrování usnadňuje.

**Správa verzí rozhraní API**

V tomto příkladu "/api/v1/products" by být směrovány do jiného řadiče než "/api/v2/products".

`/api/v1/products`
`/api/v2/products`

**Přetížené segmenty IDENTIFIKÁTORŮ URI**

V tomto příkladu "1" je číslo objednávky, ale "čekající" mapuje na kolekci.

`/orders/1`
`/orders/pending`

**Více typů parametrů**

V tomto příkladu je "1" číslo objednávky, ale "2013/06/16" určuje datum.

`/orders/1`
`/orders/2013/06/16`

<a id="enable"></a>
## <a name="enabling-attribute-routing"></a>Povolení směrování atributů

Chcete-li povolit směrování atributů, zavolejte **maphttpattributeroutes** během konfigurace. Tato metoda rozšíření je definována ve třídě **System.Web.Http.HttpConfigurationExtensions.**

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample2.cs)]

Směrování atributů lze kombinovat s [směrováním založeným na konvencích.](routing-in-aspnet-web-api.md) Chcete-li definovat trasy založené na konvencích, zavolejte metodu **MapHttpRoute.**

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample3.cs)]

Další informace o konfiguraci webového rozhraní API naleznete [v tématu Konfigurace ASP.NET webovérozhraní API 2](../advanced/configuring-aspnet-web-api.md).

<a id="config"></a>
### <a name="note-migrating-from-web-api-1"></a>Poznámka: Migrace z webového rozhraní API 1

Před web api 2 šablony projektu webového rozhraní API generované kód, jako je tento:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample4.cs)]

Pokud je povoleno směrování atributů, tento kód vyvolá výjimku. Pokud inovujete existující projekt webového rozhraní API tak, aby používal směrování atributů, nezapomeňte aktualizovat tento konfigurační kód na následující:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample5.cs?highlight=4)]

> [!NOTE]
> Další informace naleznete [v tématu Konfigurace webového rozhraní API pomocí ASP.NET hostování](../advanced/configuring-aspnet-web-api.md#webhost).

<a id="add-routes"></a>
## <a name="adding-route-attributes"></a>Přidání atributů postupu

Zde je příklad trasy definované pomocí atributu:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample6.cs)]

Řetězec &quot;zákazníci/{customerId}/orders&quot; je šablona IDENTIFIKÁTORU URI pro trasu. Webové rozhraní API se pokusí porovnat identifikátor URI požadavku se šablonou. V tomto příkladu "zákazníci" a "objednávky" jsou literálové segmenty a "{customerId}" je proměnný parametr. Následující identifikátory URI by odpovídaly této šabloně:

- `http://localhost/customers/1/orders`
- `http://localhost/customers/bob/orders`
- `http://localhost/customers/1234-5678/orders`

Párování můžete omezit pomocí [omezení popsaných](#constraints)dále v tomto tématu.

Všimněte &quot;si, že&quot; parametr {customerId} v šabloně postupu odpovídá názvu parametru *CustomerId* v metodě. Když webové rozhraní API vyvolá akci řadiče, pokusí se svázat parametry trasy. Například pokud identifikátor `http://example.com/customers/1/orders`URI je , webové rozhraní API se pokusí svázat hodnotu "1" na *customerId* parametr v akci.

Šablona identifikátoru URI může mít několik parametrů:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample7.cs)]

Všechny metody kontroleru, které nemají atribut trasy, používají směrování založené na konvencích. Tímto způsobem můžete kombinovat oba typy směrování ve stejném projektu.

## <a name="http-methods"></a>Metody PROTOKOLU HTTP

Webové rozhraní API také vybírá akce na základě metody HTTP požadavku (GET, POST atd.). Ve výchozím nastavení webové rozhraní API hledá shodu bez rozlišování velkých a malých písmen se začátkem názvu metody řadiče. Například metoda řadiče `PutCustomers` s názvem odpovídá požadavku HTTP PUT.

Tuto konvenci můžete přepsat zdobením metody následujícími atributy:

- **[HttpDelete]**
- **[HttpGet]**
- **To je v pořádku.**
- **[HttpOptions]**
- **[HttpPatch]**
- **[HttpPost]**
- **[HttpPut]**

Následující příklad mapuje metodu CreateBook na požadavky HTTP POST.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample8.cs)]

Pro všechny ostatní metody HTTP, včetně nestandardních metod, použijte atribut **AcceptVerbs,** který přebírá seznam metod HTTP.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample9.cs)]

<a id="prefixes"></a>
## <a name="route-prefixes"></a>Předpony trasy

Trasy v kontroleru často začínají stejnou předponou. Příklad:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample10.cs)]

Běžnou předponu pro celý řadič můžete nastavit pomocí atributu **[RoutePrefix]:**

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample11.cs)]

K přepsání předpony trasy použijte vlnovku (~) v atributu metody:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample12.cs)]

Předpona trasy může obsahovat parametry:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample13.cs)]

<a id="constraints"></a>
## <a name="route-constraints"></a>Omezení postupu

Omezení trasy umožňují omezit způsob, jakým jsou parametry v šabloně trasy spárovány. Obecná syntaxe &quot;je {parameter:constraint}&quot;. Příklad:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample14.cs)]

Zde bude vybrána první trasa &quot;pouze&quot; v případě, že segment id identifikátoru URI je celé číslo. V opačném případě bude zvolena druhá trasa.

V následující tabulce jsou uvedena omezení, která jsou podporována.

| Omezení | Popis | Příklad |
| --- | --- | --- |
| alpha | Odpovídá velkým nebo velkým písmenům latinky (a-z, A-Z) | {x:alfa} |
| bool | Odpovídá logické hodnotě. | {x:bool} |
| datetime | Odpovídá hodnotě **DateTime.** | {x:datetime} |
| decimal | Odpovídá desítkové hodnotě. | {x:desítkové} |
| double | Odpovídá 64bitové hodnotě s plovoucí desetinnou tácek. | {x:double} |
| float | Odpovídá 32bitové hodnotě s plovoucí desetinnou hodnotou. | {x:float} |
| Identifikátor guid | Odpovídá hodnotě GUID. | {x:guid} |
| int | Odpovídá 32bitové celočíselné hodnotě. | {x:int} |
| length | Odpovídá řetězci se zadanou délkou nebo v zadaném rozsahu délek. | {x:délka(6)} {x:délka (1,20)} |
| long | Odpovídá 64bitové celočíselné hodnotě. | {x:long} |
| max | Odpovídá celé číslo s maximální hodnotou. | {x:max(10)} |
| Maxlength | Odpovídá řetězci s maximální délkou. | {x:maxlength(10)} |
| min | Odpovídá celé číslo s minimální hodnotou. | {x:min(10)} |
| Minlength | Odpovídá řetězci s minimální délkou. | {x:minlength(10)} |
| range | Odpovídá celé číslo v rozsahu hodnot. | {x:rozsah (10,50)} |
| Regex | Odpovídá regulárnímu výrazu. | {x:regex(^\d{3}-\d{3}-\d{4}_)} |

Všimněte si, že některá &quot;omezení, například min&quot;, přijmout argumenty v závorce. Na parametr oddělený dvojtečkou můžete použít více omezení.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample15.cs)]

### <a name="custom-route-constraints"></a>Vlastní omezení postupu

Vlastní omezení trasy můžete vytvořit implementací rozhraní **IHttpRouteConstraint.** Například následující omezení omezuje parametr na nenulovou celočíselnou hodnotu.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample16.cs)]

Následující kód ukazuje, jak zaregistrovat omezení:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample17.cs)]

Nyní můžete použít omezení ve svých trasách:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample18.cs)]

Můžete také nahradit celou třídu **DefaultInlineConstraintResolver** implementací rozhraní **IInlineConstraintResolver.** Tím nahradí všechny předdefinované omezení, pokud implementace **IInlineConstraintResolver** konkrétně přidá je.

<a id="optional"></a>
## <a name="optional-uri-parameters-and-default-values"></a>Volitelné parametry identifikátoru URI a výchozí hodnoty

Parametr URI můžete provést jako volitelný přidáním otazníku k parametru trasy. Pokud je parametr trasy volitelný, musíte definovat výchozí hodnotu parametru metody.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample19.cs)]

V tomto `/api/books/locale/1033` příkladu a `/api/books/locale` vrátit stejný prostředek.

Alternativně můžete zadat výchozí hodnotu uvnitř šablony trasy takto:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample20.cs)]

To je téměř stejný jako v předchozím příkladu, ale je mírný rozdíl chování při použití výchozí hodnoty.

- V prvním příkladu ("{lcid:int?}"), výchozí hodnota 1033 je přiřazena přímo parametru metody, takže parametr bude mít tuto přesnou hodnotu.
- V druhém příkladu ("{lcid:int=1033}) prochází výchozí hodnota "1033" procesem vazby modelu. Výchozí pořadač modelu převede "1033" na číselnou hodnotu 1033. Můžete však připojit vlastní pořadač modelu, který by mohl udělat něco jiného.

(Ve většině případů, pokud nemáte vlastní model pořadače v kanálu, dva formuláře budou ekvivalentní.)

<a id="route-names"></a>
## <a name="route-names"></a>Názvy tras

Ve webovém rozhraní API má každá trasa název. Názvy tras jsou užitečné pro generování propojení, takže můžete zahrnout odkaz do odpovědi HTTP.

Chcete-li zadat název trasy, nastavte vlastnost **Name** u atributu. Následující příklad ukazuje, jak nastavit název trasy a také jak použít název trasy při generování propojení.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample21.cs)]

<a id="order"></a>
## <a name="route-order"></a>Pořadí postupu

Když se rozhraní pokusí porovnat identifikátor URI s postupem, vyhodnotí trasy v určitém pořadí. Chcete-li zadat pořadí, nastavte vlastnost **Order** v atributu trasy. Nižší hodnoty jsou vyhodnoceny jako první. Výchozí hodnota objednávky je nula.

Zde je, jak je určeno celkové pořadí:

1. Porovnejte **vlastnost Order** atributu route.
2. Podívejte se na každý segment identifikátoru URI v šabloně trasy. Pro každý segment postupujte takto:

    1. Doslovné segmenty.
    2. Parametry trasy s omezeními.
    3. Parametry trasy bez omezení.
    4. Segmenty parametrů zástupných symbolů s vazbami.
    5. Segmenty parametrů se zástupnými symboly bez omezení.
3. V případě nerozhodného spojení jsou trasy seřazeny podle porovnání ordinálních řetězců bez rozlišování velkých a malých písmen ([OrdinalIgnoreCase](https://msdn.microsoft.com/library/system.stringcomparer.ordinalignorecase.aspx)) šablony trasy.

Zde je příklad. Předpokládejme, že definujete následující řadič:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample22.cs)]

Tyto trasy jsou seřazeny následujícím způsobem.

1. objednávky/podrobnosti
2. objednávky/{id}
3. objednávky/{customerName}
4. objednávky/{\*datum}
5. objednávky/nevyřízené

Všimněte si, že "podrobnosti" je doslovný segment a zobrazí se před "{id}", ale "čekající" se zobrazí jako poslední, protože **Order** vlastnost je 1. (Tento příklad předpokládá, že neexistují žádní zákazníci s názvem "podrobnosti" nebo "čeká na vyřízení". Obecně se snažte vyhnout nejednoznačným trasami. V tomto příkladu `GetByCustomer` je lepší šablonou postupu "customers/{customerName}" )
