---
uid: mvc/overview/getting-started/introduction/adding-search
title: Hledat | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/17/2019
ms.assetid: df001954-18bf-4550-b03d-43911a0ea186
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-search
msc.type: authoredcontent
ms.openlocfilehash: be4e4d13e574b0fcb77d2d0fb8c6f58041b1ece2
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044847"
---
# <a name="search"></a>Search

[!INCLUDE [consider RP](~/includes/razor.md)]

## <a name="adding-a-search-method-and-search-view"></a>Přidání vyhledávací metody a zobrazení vyhledávání

V této části přidáte funkci hledání do `Index` metody Action, která umožňuje hledat filmy podle žánru nebo názvu.

## <a name="prerequisites"></a>Předpoklady

Aby bylo možné spárovat snímky obrazovky této části, je nutné spustit aplikaci (F5) a přidat následující filmy do databáze.

| Nadpis | Datum vydání | Žánru | Cena |
| ----- | ------------ | ----- | ----- |
| Ghostbusters | 6/8/1984 | Komedie | 6,99 |
| Ghostbusters II | 6/16/1989 | Komedie | 6,99 |
| Globálním Apes | 3/27/1986 | Akce | 5.99 |

## <a name="updating-the-index-form"></a>Aktualizace formuláře indexu

Začněte aktualizací `Index` metody Action na existující `MoviesController` třídu. Zde je kód:

[!code-csharp[Main](adding-search/samples/sample1.cs?highlight=1,6-9)]

První řádek `Index` metody vytvoří následující dotaz [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) pro výběr filmů:

[!code-csharp[Main](adding-search/samples/sample2.cs)]

V tomto okamžiku je definován dotaz, ale ještě nebyl v databázi spuštěn.

Pokud `searchString` parametr obsahuje řetězec, dotaz na filmy je upraven pro filtrování podle hodnoty hledaného řetězce, a to pomocí následujícího kódu:

[!code-csharp[Main](adding-search/samples/sample3.cs)]

`s => s.Title`Výše uvedený kód je [výraz lambda](https://msdn.microsoft.com/library/bb397687.aspx). Výrazy lambda se používají v dotazech [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) založených na metodách jako argumenty standardních metod operátoru dotazu, jako je metoda [WHERE](https://msdn.microsoft.com/library/system.linq.enumerable.where.aspx) použitá ve výše uvedeném kódu. Dotazy LINQ nejsou provedeny při jejich definování nebo při jejich úpravě voláním metody, jako je `Where` nebo `OrderBy` . Místo toho je provádění dotazu odloženo, což znamená, že vyhodnocení výrazu je zpožděno, dokud se jeho realizovaná hodnota neopakuje nebo je [`ToList`](https://msdn.microsoft.com/library/bb342261.aspx) volána metoda. V `Search` ukázce je dotaz spuštěn v zobrazení *index. cshtml* . Další informace o odložení provádění dotazů naleznete v tématu [provádění dotazů](https://msdn.microsoft.com/library/bb738633.aspx).

> [!NOTE]
> Metoda [Contains](https://msdn.microsoft.com/library/bb155125.aspx) je spuštěna v databázi, nikoli kód jazyka c# výše. V databázi [obsahuje](https://msdn.microsoft.com/library/bb155125.aspx) mapy [typu SQL jako](https://msdn.microsoft.com/library/ms179859.aspx), což rozlišuje velká a malá písmena.

Nyní můžete aktualizovat `Index` zobrazení, které zobrazí formulář uživateli.

Spusťte aplikaci a přejděte na */Movies/index*. Připojit řetězec dotazu, například `?searchString=ghost` k adrese URL. Zobrazí se filtrované filmy.

![SearchQryStr](adding-search/_static/image1.png)

Změníte-li podpis `Index` metody tak, aby měl parametr s názvem `id` , `id` parametr bude odpovídat `{id}` zástupnému symbolu pro výchozí trasy nastavené v souboru *App \_ Start\RouteConfig.cs* .

[!code-json[Main](adding-search/samples/sample4.txt)]

Původní `Index` metoda vypadá takto::

[!code-csharp[Main](adding-search/samples/sample5.cs)]

Upravená `Index` Metoda by vypadala takto:

[!code-csharp[Main](adding-search/samples/sample6.cs?highlight=1,3)]

Nyní můžete název hledání předat jako data trasy (segment adresy URL) místo jako hodnotu řetězce dotazu.

![](adding-search/_static/image2.png)

Nemůžete ale očekávat, že uživatelé můžou upravovat adresu URL pokaždé, když chtějí hledat film. Takže teď přidáte uživatelské rozhraní, které jim umožní filtrovat filmy. Pokud jste změnili podpis `Index` metody pro testování způsobu předání parametru ID vázaného na trasu, změňte jej tak, aby `Index` Metoda přebírá řetězcový parametr s názvem `searchString` :

[!code-csharp[Main](adding-search/samples/sample7.cs)]

Otevřete soubor *Views\Movies\Index.cshtml* a hned za `@Html.ActionLink("Create New", "Create")` přidejte značku formuláře zvýrazněné níže:

[!code-cshtml[Main](adding-search/samples/sample8.cshtml?highlight=12-15)]

`Html.BeginForm`Pomocná rutina vytvoří počáteční `<form>` značku. `Html.BeginForm`Pomocná osoba způsobí odeslání formuláře do sebe sama, když ho uživatel odešle kliknutím na tlačítko **Filtr** .

Při zobrazení a úpravách souborů zobrazení má Visual Studio 2013 dobrým vylepšením. Když aplikaci spustíte s otevřeným zobrazením souboru, Visual Studio 2013 vyvolá správnou metodu akce kontroleru pro zobrazení zobrazení.

![](adding-search/_static/image3.png)

Otevřete zobrazení index v aplikaci Visual Studio (jak je znázorněno na obrázku výše), klepnutím na centrum F5 nebo F5 spusťte aplikaci a potom zkuste vyhledat film.

![](adding-search/_static/image4.png)

Neexistuje `HttpPost` přetížení `Index` metody. Nepotřebujete ho, protože metoda nemění stav aplikace, stačí data filtrovat.

Můžete přidat následující `HttpPost Index` metodu. V takovém případě by se akce původce shodovala s `HttpPost Index` metodou a `HttpPost Index` Metoda by běžela, jak je znázorněno na následujícím obrázku.

[!code-csharp[Main](adding-search/samples/sample9.cs)]

![SearchPostGhost](adding-search/_static/image5.png)

Nicméně i v případě, že přidáte tuto `HttpPost` verzi `Index` metody, existuje omezení, jak je vše implementováno. Představte si, že chcete vytvořit záložku konkrétního hledání nebo chcete poslat odkaz na přátele, na které můžou kliknout, aby se zobrazil stejný filtrovaný seznam filmů. Všimněte si, že adresa URL požadavku HTTP POST je stejná jako adresa URL žádosti GET (localhost: xxxxx/video/index) – v samotné adrese URL nejsou žádné vyhledávací informace. Nyní jsou informace o hledaném řetězci odesílány na server jako hodnota pole formuláře. To znamená, že nemůžete zachytit informace o hledání do záložky nebo odeslat přátelům v adrese URL.

Řešením je použití přetížení `BeginForm` , které určuje, že žádost post by měla do adresy URL přidat informace o hledání a že by měla být směrována na `HttpGet` verzi `Index` metody. Nahraďte existující metodu bez parametrů `BeginForm` následujícím kódem:

[!code-cshtml[Main](adding-search/samples/sample10.cshtml)]

![BeginFormPost_SM](adding-search/_static/image6.png)

Když teď odešlete hledání, adresa URL obsahuje řetězec vyhledávacího dotazu. Hledání bude také jít na `HttpGet Index` metodu Action, i když máte `HttpPost Index` metodu.

![IndexWithGetURL](adding-search/_static/image7.png)

## <a name="adding-search-by-genre"></a>Přidávání hledání podle žánru

Pokud jste přidali `HttpPost` verzi `Index` metody, odstraňte ji nyní.

V dalším kroku přidáte funkci, která uživatelům umožní Hledat filmy podle žánru. Nahraďte metodu `Index` následujícím kódem:

[!code-csharp[Main](adding-search/samples/sample11.cs)]

Tato verze `Index` metody přebírá další parametr, konkrétně `movieGenre` . První pár řádků kódu vytvoří `List` objekt pro uchování filmových žánrů z databáze.

Následující kód je dotaz LINQ, který načte všechny žánry z databáze.

[!code-csharp[Main](adding-search/samples/sample12.cs)]

Kód používá `AddRange` metodu obecné `List` kolekce k přidání všech různých žánrů do seznamu. (Bez `Distinct` modifikátoru by se přidaly duplicitní žánry – například komedie by se přidalo dvakrát v našem příkladu). Kód pak uloží seznam žánrů v `ViewBag.MovieGenre` objektu. Při ukládání dat kategorií (například filmových žánrů) jako objektu [SelectList](https://msdn.microsoft.cus/library/system.web.mvc.selectlist(v=vs.108).aspx) do `ViewBag` pole je přístup k datům kategorie v rozevíracím seznamu typický pro aplikace MVC.

Následující kód ukazuje, jak ověřit `movieGenre` parametr. Pokud není prázdný, kód dál omezí dotaz na filmy, aby vybral vybrané filmy na zadaný Žánr.

[!code-csharp[Main](adding-search/samples/sample13.cs)]

Jak bylo uvedeno dříve, dotaz není spuštěn v databázi, dokud se seznam filmů neopakuje (k tomu dojde v zobrazení, po `Index` návratu metody Action).

## <a name="adding-markup-to-the-index-view-to-support-search-by-genre"></a>Přidání značek do zobrazení indexu pro podporu hledání podle žánru

Přidejte `Html.DropDownList` pomocníka do souboru *Views\Movies\Index.cshtml* těsně před `TextBox` pomocnou rutinou. Dokončený kód je uveden níže:

[!code-cshtml[Main](adding-search/samples/sample14.cshtml?highlight=11)]

V následujícím kódu:

[!code-cshtml[Main](adding-search/samples/sample15.cshtml)]

Parametr "MovieGenre" poskytuje klíč, pomocí kterého může `DropDownList` Pomocník najít `IEnumerable<SelectListItem>` v `ViewBag` . `ViewBag`Byla naplněna v metodě Action:

[!code-csharp[Main](adding-search/samples/sample16.cs?highlight=10)]

Parametr all poskytuje popisek možnosti. Pokud v prohlížeči zkontrolujete tuto volbu, uvidíte, že její atribut "value" je prázdný. Vzhledem k tomu, že náš řadič filtruje pouze `if` řetězec `null` , není ani prázdný, odesláním prázdné hodnoty `movieGenre` zobrazíte všechny žánry.

Můžete také nastavit možnost, která bude standardně vybrána. Pokud jste jako výchozí možnost chtěli "komedie", změnili byste kód v řadiči, například:

[!code-cshtml[Main](adding-search/samples/sample17.cshtml)]

Spusťte aplikaci a přejděte na */Movies/index*. Zkuste hledat podle žánru, podle názvu filmu a podle obou kritérií.

![](adding-search/_static/image8.png)

V této části jste vytvořili metodu a zobrazení akce hledání, které umožní uživatelům hledat podle názvu a žánru. V další části se podíváte na postup přidání vlastnosti do `Movie` modelu a postup přidání inicializátoru, který automaticky vytvoří testovací databázi.

> [!div class="step-by-step"]
> [Předchozí](examining-the-edit-methods-and-edit-view.md) 
>  [Další](adding-a-new-field.md)
