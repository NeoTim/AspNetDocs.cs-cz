---
uid: web-api/overview/web-api-routing-and-actions/create-a-rest-api-with-attribute-routing
title: Vytvoření REST API s směrováním atributů ve webovém rozhraní API 2 pro ASP.NET | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/26/2013
ms.assetid: 23fc77da-2725-4434-99a0-ff872d96336b
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/create-a-rest-api-with-attribute-routing
msc.type: authoredcontent
ms.openlocfilehash: 6eac36767bf34857d5341188d0653e7fec7cade2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "86188796"
---
# <a name="create-a-rest-api-with-attribute-routing-in-aspnet-web-api-2"></a>Vytvoření REST API s směrováním atributů ve webovém rozhraní API 2 pro ASP.NET

o [Jan Wasson](https://github.com/MikeWasson)

Webové rozhraní API 2 podporuje nový typ směrování, kterému se říká *Směrování atributů*. Obecný přehled směrování atributů najdete v tématu [Směrování atributů ve webovém rozhraní API 2](attribute-routing-in-web-api-2.md). V tomto kurzu budete používat směrování atributů k vytvoření REST API pro kolekci knih. Rozhraní API bude podporovat tyto akce:

| Akce | Příklad identifikátoru URI |
| --- | --- |
| Získá seznam všech knih. | /api/books |
| Získat knihu podle ID | /api/books/1 |
| Získejte podrobnosti knihy. | /api/books/1/details |
| Získá seznam knih podle žánru. | /api/books/fantasy |
| Získá seznam knih podle data publikování. | /API/Books/Date/2013-02-16/API/Books/Date/2013/02/16 (alternativní formulář) |
| Získá seznam knih podle konkrétního autora. | /api/authors/1/books |

Všechny metody jsou jen pro čtení (požadavky HTTP GET).

Pro datovou vrstvu budeme používat Entity Framework. Záznamy o knihách budou obsahovat následující pole:

- ID
- Nadpis
- Žánru
- Datum publikace
- Cena
- Popis
- AuthorID (cizí klíč pro tabulku autorů)

Pro většinu požadavků ale rozhraní API vrátí podmnožinu těchto dat (název, autor a Žánr). Chcete-li získat úplný záznam, požadavky klienta `/api/books/{id}/details` .

## <a name="prerequisites"></a>Požadavky

[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Komunita, edice Professional nebo Enterprise.

## <a name="create-the-visual-studio-project"></a>Vytvoření projektu sady Visual Studio

Začněte spuštěním sady Visual Studio. V nabídce **soubor** vyberte **Nový** a pak vyberte **projekt**.

Rozbalte položku **nainstalovanou**  >  kategorii**Visual C#** . V části **Visual C#** vyberte **Web**. V seznamu šablon projektu vyberte **ASP.NET webová aplikace (.NET Framework)**. Pojmenujte projekt &quot; BooksAPI &quot; .

![](create-a-rest-api-with-attribute-routing/_static/image1.png)

V dialogovém okně **Nová webová aplikace ASP.NET** vyberte **prázdnou** šablonu. V části Přidat složky a základní reference pro klikněte zaškrtněte políčko **webové rozhraní API** . Klikněte na **OK**.

![](create-a-rest-api-with-attribute-routing/_static/image2.png)

Tím se vytvoří kostra projektu, který je nakonfigurován pro funkce webového rozhraní API.

### <a name="domain-models"></a>Doménové modely

Dále přidejte třídy pro doménové modely. V Průzkumník řešení klikněte pravým tlačítkem na složku modely. Vyberte **Přidat**a pak vybrat **třídu**. Pojmenujte třídu `Author` .

![](create-a-rest-api-with-attribute-routing/_static/image3.png)

Nahraďte kód v Author.cs následujícím způsobem:

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample1.cs)]

Nyní přidejte další třídu s názvem `Book` .

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample2.cs)]

### <a name="add-a-web-api-controller"></a>Přidat kontroler webového rozhraní API

V tomto kroku přidáme kontroler webového rozhraní API, který používá Entity Framework jako datovou vrstvu.

Sestavte projekt stisknutím kombinace kláves CTRL+SHIFT+B. Entity Framework používá reflexi ke zjištění vlastností modelů, takže vyžaduje zkompilované sestavení pro vytvoření schématu databáze.

V Průzkumník řešení klikněte pravým tlačítkem myši na složku Controllers. Vyberte **Přidat**a pak vybrat **kontroler**.

![](create-a-rest-api-with-attribute-routing/_static/image4.png)

V dialogovém okně **Přidat generování uživatelského rozhraní** vyberte **KONTROLER webového rozhraní API 2 s akcemi pomocí Entity Framework**.

[![](create-a-rest-api-with-attribute-routing/_static/image6.png)](create-a-rest-api-with-attribute-routing/_static/image5.png)

V dialogovém okně **Přidat řadič** jako **název kontroleru**zadejte &quot; BooksController &quot; . Zaškrtněte &quot; políčko použít akce asynchronního kontroleru &quot; . V případě **třídy model**vyberte možnost &quot; Kniha &quot; . (Pokud nevidíte `Book` třídu uvedenou v rozevíracím seznamu, ujistěte se, že jste projekt sestavili.) Pak klikněte na tlačítko "+".

![](create-a-rest-api-with-attribute-routing/_static/image7.png)

V dialogovém okně **nový kontext dat** klikněte na **Přidat** .

![](create-a-rest-api-with-attribute-routing/_static/image8.png)

V dialogovém okně **Přidat řadič** klikněte na **Přidat** . Generování uživatelského rozhraní přidá třídu s názvem `BooksController` , která definuje kontroler rozhraní API. Přidá také třídu s názvem `BooksAPIContext` ve složce modely, která definuje kontext dat pro Entity Framework.

![](create-a-rest-api-with-attribute-routing/_static/image9.png)

### <a name="seed-the-database"></a>Přidání dat do databáze

V nabídce Nástroje vyberte **Správce balíčků NuGet**a pak vyberte **Konzola správce balíčků**.

V okně konzoly Správce balíčků zadejte následující příkaz:

[!code-powershell[Main](create-a-rest-api-with-attribute-routing/samples/sample3.ps1)]

Tento příkaz vytvoří složku migrace a přidá nový soubor kódu s názvem Configuration.cs. Otevřete tento soubor a přidejte následující kód do `Configuration.Seed` metody.

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample4.cs)]

V okně konzoly Správce balíčků zadejte následující příkazy.

[!code-powershell[Main](create-a-rest-api-with-attribute-routing/samples/sample5.ps1)]

Tyto příkazy vytvoří místní databázi a vyvolávají metodu počáteční hodnoty k naplnění databáze.

![](create-a-rest-api-with-attribute-routing/_static/image10.png)

## <a name="add-dto-classes"></a>Přidat třídy DTO

Pokud aplikaci teď spustíte a odešlete požadavek GET na/API/Books/1, odpověď vypadá podobně jako v následujícím příkladu. (Přidal (a) jsem odsazení pro čitelnost.)

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample6.json)]

Místo toho chci, aby tento požadavek vrátil podmnožinu polí. Také chci, aby vracel jméno autora, nikoli ID autora. K tomuto účelu upraví metody kontroleru tak, aby vracely *objekt pro přenos dat* (DTO) místo modelu EF. DTO je objekt, který je určen pouze k přenosu dat.

V Průzkumník řešení klikněte pravým tlačítkem myši na projekt a vyberte **Přidat**  |  **novou složku**. Pojmenujte složku &quot; DTO &quot; . Přidejte třídu s názvem `BookDto` do složky DTO s následující definicí:

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample7.cs)]

Přidejte další třídu s názvem `BookDetailDto` .

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample8.cs)]

Dále aktualizujte `BooksController` třídu tak, aby vracela `BookDto` instance. Pro projekty instancí do instancí použijeme metodu [Queryable. Select](https://msdn.microsoft.com/library/system.linq.queryable.select.aspx) . `Book` `BookDto` Zde je aktualizovaný kód pro třídu Controller.

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample9.cs)]

> [!NOTE]
> Odstranil `PutBook` (a) `PostBook` metody, `DeleteBook` protože nejsou pro tento kurz potřeba.

Když teď aplikaci spustíte a vyžádáte/API/Books/1, tělo odpovědi by mělo vypadat takto:

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample10.json)]

## <a name="add-route-attributes"></a>Přidat atributy směrování

Dále převedeme kontroler na použití směrování atributů. Nejprve do kontroleru přidejte atribut **RoutePrefix** . Tento atribut definuje počáteční segmenty identifikátorů URI pro všechny metody tohoto kontroleru.

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample11.cs?highlight=1)]

Pak přidejte atributy **[Route]** k akcím kontroleru následujícím způsobem:

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample12.cs?highlight=1,7)]

Šablona trasy pro každou metodu kontroleru je předponou a řetězcem zadaným v atributu **Route** . Pro `GetBook` metodu zahrnuje šablona trasy parametrizovaný řetězec &quot; {ID: int} &quot; , který odpovídá, pokud segment identifikátoru URI obsahuje celočíselnou hodnotu.

| Metoda | Šablona směrování | Příklad identifikátoru URI |
| --- | --- | --- |
| `GetBooks` | rozhraní API/knihy | `http://localhost/api/books` |
| `GetBook` | API/Books/{ID: int} | `http://localhost/api/books/5` |

## <a name="get-book-details"></a>Získat podrobnosti knihy

Aby bylo možné získat podrobnosti o knize, odešle klient požadavek GET na `/api/books/{id}/details` , kde *{ID}* je ID knihy.

Do třídy přidejte následující metodu `BooksController` .

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample13.cs)]

Pokud si vyžádáte `/api/books/1/details` , odpověď vypadá nějak takto:

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample14.json)]

## <a name="get-books-by-genre"></a>Získat knihy podle žánru

Pokud chcete získat seznam knih v konkrétním žánru, pošle klient požadavek GET na `/api/books/genre` , kde *Žánr* je název žánru. (Například `/api/books/fantasy` .)

Přidejte následující metodu do `BooksController` .

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample15.cs)]

Tady definujeme trasu, která obsahuje parametr {Žánr} v šabloně identifikátoru URI. Všimněte si, že webové rozhraní API dokáže rozlišovat tyto dva identifikátory URI a směrovat je do různých metod:

`/api/books/1`

`/api/books/fantasy`

Důvodem je, že `GetBook` Metoda obsahuje omezení, že segment "ID" musí být celočíselná hodnota:

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample16.cs?highlight=1)]

Pokud si vyžádáte/API/Books/fantasy, odpověď vypadá nějak takto:

`[ { "Title": "Midnight Rain", "Author": "Ralls, Kim", "Genre": "Fantasy" }, { "Title": "Maeve Ascendant", "Author": "Corets, Eva", "Genre": "Fantasy" }, { "Title": "The Sundered Grail", "Author": "Corets, Eva", "Genre": "Fantasy" } ]`

## <a name="get-books-by-author"></a>Získat knihy podle autora

Chcete-li získat seznam knih pro určitého autora, klient odešle požadavek GET na adresu `/api/authors/id/books` , kde *ID* je ID autora.

Přidejte následující metodu do `BooksController` .

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample17.cs)]

Tento příklad je zajímavý, protože &quot; knihy &quot; se považují za podřízený prostředek &quot; autorů &quot; . Tento model je poměrně společný v rozhraních API RESTful.

Znak tilda (~) v šabloně trasy Přepisuje předponu trasy v atributu **RoutePrefix** .

## <a name="get-books-by-publication-date"></a>Získat knihy podle data publikování

Chcete-li získat seznam knih podle data publikování, klient odešle požadavek GET na `/api/books/date/yyyy-mm-dd` , kde *RRRR-MM-DD* je datum.

Tady je jeden ze způsobů, jak to provést:

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample18.cs)]

`{pubdate:datetime}`Parametr je omezený, aby odpovídal hodnotě **DateTime** . Tato funkce funguje, ale ve skutečnosti je to více opravňující než vám. Například tyto identifikátory URI budou odpovídat i trase:

`/api/books/date/Thu, 01 May 2008`

`/api/books/date/2000-12-16T00:00:00`

S povolením těchto identifikátorů URI není nic špatné. Můžete však omezit směrování na konkrétní formát přidáním omezení regulárního výrazu do šablony trasy:

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample19.cs?highlight=1)]

Nyní se budou shodovat pouze kalendářní data ve formě &quot; yyyy-MM-DD &quot; . Všimněte si, že pro ověření, že máme reálné datum, nepoužíváme regulární výraz. Tato hodnota je zpracována, když se webové rozhraní API pokusí převést segment identifikátoru URI na instanci **DateTime** . Neplatné datum, jako je například ' 2012-47-99 ', nebude převedeno a klient obdrží chybu 404.

Můžete také podporovat oddělovač lomítka ( `/api/books/date/yyyy/mm/dd` ) přidáním dalšího atributu **[Route]** s jiným regulárním výrazem.

[!code-html[Main](create-a-rest-api-with-attribute-routing/samples/sample20.html)]

Tady je jen malý, ale důležitý detail. Druhá šablona trasy obsahuje zástupný znak ( \* ) na začátku parametru {pubdate}:

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample21.json)]

Tím se oznámí směrovacímu modulu, že {pubdate} by se měl shodovat se zbytkem identifikátoru URI. Ve výchozím nastavení je parametr šablony shodný s jedním segmentem identifikátoru URI. V tomto případě chceme, aby {pubdate} zahrnoval několik segmentů identifikátorů URI:

`/api/books/date/2013/06/17`

## <a name="controller-code"></a>Kód kontroleru

Zde je kompletní kód pro třídu BooksController.

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample22.cs)]

## <a name="summary"></a>Shrnutí

Směrování atributů poskytuje větší kontrolu a větší flexibilitu při navrhování identifikátorů URI pro vaše rozhraní API.
