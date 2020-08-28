---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/examining-the-edit-methods-and-edit-view
title: Zkoumání metod Edit a zobrazení pro úpravy (C#) | Microsoft Docs
author: Rick-Anderson
description: V tomto kurzu se seznámíte se základy vytváření webových aplikací ASP.NET MVC pomocí nástroje Microsoft Visual Web Developer 2010 Express Service Pack 1, který je...
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 1d266bf0-a61e-423b-a3d2-13773d7dafe2
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/examining-the-edit-methods-and-edit-view
msc.type: authoredcontent
ms.openlocfilehash: baa300c66bfae9fe602a8fe597e21b0abbaf3a63
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044984"
---
# <a name="examining-the-edit-methods-and-edit-view-c"></a>Zkoumání metod Edit a zobrazení pro úpravy (C#)

od [Rick Anderson](https://twitter.com/RickAndMSFT)

> > [!NOTE]
> > K [dispozici je](../../../getting-started/introduction/getting-started.md) aktualizovaná verze tohoto kurzu, která používá ASP.NET MVC 5 a Visual Studio 2013. Je to bezpečnější, mnohem jednodušší a ukazuje více funkcí.
> 
> 
> V tomto kurzu se seznámíte se základy vytváření webových aplikací ASP.NET MVC pomocí nástroje Microsoft Visual Web Developer 2010 Express Service Pack 1, což je bezplatná verze Microsoft Visual Studio. Než začnete, ujistěte se, že jste nainstalovali požadavky uvedené níže. Všechny z nich můžete nainstalovat kliknutím na následující odkaz: instalace [webové platformy](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack). Případně můžete požadavky jednotlivě nainstalovat pomocí následujících odkazů:
> 
> - [Požadavky sady Visual Studio Web Developer Express SP1](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [Aktualizace nástrojů MVC 3 pro ASP.NET](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4,0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(podpora modulu runtime + nástroje)
> 
> Pokud používáte sadu Visual Studio 2010 místo sady Visual Web Developer 2010, nainstalujte požadavky kliknutím na následující odkaz: sady [Visual studio 2010 požadavky](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).
> 
> Projekt Visual Web Developer se zdrojovým kódem C# je k dispozici pro toto téma. [Stáhněte si verzi jazyka C#](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098). Pokud dáváte přednost Visual Basic, přepněte se na [Visual Basic verzi](../vb/intro-to-aspnet-mvc-3.md) tohoto kurzu.

V této části proberete vygenerované metody a zobrazení akcí pro kontroler videí. Pak přidáte vlastní vyhledávací stránku.

Spusťte aplikaci a přejděte na `Movies` kontroler připojením */Movies* k adrese URL v adresním řádku prohlížeče. Podržte ukazatel myši na odkaz pro **Úpravy** a zobrazte tak adresu URL, na kterou odkazuje.

[![EditLink_sm](examining-the-edit-methods-and-edit-view/_static/image2.png)](examining-the-edit-methods-and-edit-view/_static/image1.png)

Odkaz **Edit** byl vygenerován `Html.ActionLink` metodou v zobrazení *Views\Movies\Index.cshtml* :

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample1.cshtml)]

[![HTML. ActionLink](examining-the-edit-methods-and-edit-view/_static/image4.png)](examining-the-edit-methods-and-edit-view/_static/image3.png)

`Html`Objekt je pomocník, který je vystaven pomocí vlastnosti `WebViewPage` základní třídy. `ActionLink`Metoda pomocné rutiny usnadňuje dynamické generování hypertextových odkazů HTML, které odkazují na metody akcí na řadičích. Prvním argumentem `ActionLink` metody je text odkazu, který se má vykreslit (například `<a>Edit Me</a>` ). Druhý argument je název metody akce, která má být vyvolána. Konečný argument je [anonymní objekt](https://weblogs.asp.net/scottgu/archive/2007/05/15/new-orcas-language-feature-anonymous-types.aspx) , který generuje data trasy (v tomto případě ID 4).

Vygenerovaný odkaz uvedený na předchozím obrázku je `http://localhost:xxxxx/Movies/Edit/4` . Výchozí trasa přijímá vzor adresy URL `{controller}/{action}/{id}` . Proto ASP.NET převede `http://localhost:xxxxx/Movies/Edit/4` požadavek na `Edit` metodu akce `Movies` kontroleru s parametrem, který se `ID` rovná 4.

Můžete také předat parametry metody akce pomocí řetězce dotazu. Například adresa URL `http://localhost:xxxxx/Movies/Edit?ID=4` také předá parametr `ID` 4 `Edit` metodě Action `Movies` kontroleru.

[![EditQueryString](examining-the-edit-methods-and-edit-view/_static/image6.png)](examining-the-edit-methods-and-edit-view/_static/image5.png)

Otevřete `Movies` kontroler. Následující dvě `Edit` metody akce jsou uvedeny níže.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample2.cs)]

Všimněte si, že druhá `Edit` Metoda Action předchází `HttpPost` atribut. Tento atribut určuje, že přetížení `Edit` metody lze vyvolat pouze pro požadavky post. Můžete použít `HttpGet` atribut na první metodu Edit, ale to není nutné, protože je to výchozí. (Odkazujeme na metody akcí, které implicitně přiřazují `HttpGet` atribut jako `HttpGet` metody.)

`HttpGet` `Edit` Metoda přebírá parametr ID filmu, vyhledá film pomocí `Find` metody Entity Framework a vrátí vybraný film do zobrazení pro úpravy. Když systém generování uživatelského rozhraní vytvořil zobrazení pro úpravy, zkontroloval `Movie` třídu a vytvořil kód pro vykreslení `<label>` a `<input>` prvky pro každou vlastnost třídy. Následující příklad ukazuje zobrazení pro úpravy, které bylo vygenerováno:

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample3.cshtml)]

Všimněte si, jak šablona zobrazení obsahuje `@model MvcMovie.Models.Movie` příkaz v horní části souboru – určuje, že zobrazení očekává, že model pro šablonu zobrazení bude typu `Movie` .

Generovaný kód používá několik *pomocných metod* pro zjednodušení značek HTML. [`Html.LabelFor`](https://msdn.microsoft.com/library/gg401864(VS.98).aspx)Pomocník zobrazuje název pole ("title", "ReleaseDate", "Žánr" nebo "Price"). [`Html.EditorFor`](https://msdn.microsoft.com/library/system.web.mvc.html.editorextensions.editorfor(VS.98).aspx)Pomocník zobrazí prvek jazyka HTML `<input>` . [`Html.ValidationMessageFor`](https://msdn.microsoft.com/library/system.web.mvc.html.validationextensions.validationmessagefor(VS.98).aspx)Pomocník zobrazuje všechny ověřovací zprávy přidružené k této vlastnosti.

Spusťte aplikaci a přejděte na adresu URL */Movies* . Klikněte na odkaz **Upravit** . V prohlížeči zobrazte zdroj stránky. KÓD HTML na stránce vypadá podobně jako v následujícím příkladu. (Pro přehlednost bylo vyloučeno označení nabídky.)

[!code-html[Main](examining-the-edit-methods-and-edit-view/samples/sample4.html)]

`<input>`Prvky jsou v elementu HTML, `<form>` jehož `action` atribut je nastaven na hodnotu post na adresu URL */Movies/Edit* . Po kliknutí na tlačítko pro **Úpravy** budou data formuláře odeslána na server.

## <a name="processing-the-post-request"></a>Zpracovává se žádost POST.

Následující výpis zobrazuje `HttpPost` verzi `Edit` metody Action.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample5.cs)]

Pořadač modelu ASP.NET Framework přebírá hodnoty v zaúčtovaném formuláři a vytvoří `Movie` objekt, který se předává jako `movie` parametr. `ModelState.IsValid`Vrácení se změnami v kódu ověřuje, že data odeslaná ve formuláři lze použít k úpravě `Movie` objektu. Pokud jsou data platná, kód uloží filmová data do `Movies` kolekce `MovieDBContext` instancí. Kód pak uloží nová filmová data do databáze voláním `SaveChanges` metody `MovieDBContext` , která uchovává změny v databázi. Po uložení dat kód přesměruje uživatele na `Index` metodu akce `MoviesController` třídy, což způsobí, že se aktualizovaný film zobrazí v seznamu filmů.

Pokud nejsou publikované hodnoty platné, budou ve formuláři znovu zobrazeny. U `Html.ValidationMessageFor` pomocníků v šabloně zobrazení *Edit. cshtml* se postará o zobrazení příslušných chybových zpráv.

[![abcNotValid](examining-the-edit-methods-and-edit-view/_static/image8.png)](examining-the-edit-methods-and-edit-view/_static/image7.png)

> **Poznámka o národních prostředích** Pokud běžně pracujete s národním prostředím jiným než angličtinu, přečtěte si téma [Podpora ověřování ASP.NET MVC 3 pomocí jiných než anglických národních prostředí.](https://msdn.microsoft.com/library/gg674880(VS.98).aspx)

## <a name="making-the-edit-method-more-robust"></a>Zvýšení odolnosti metody úprav

`HttpGet` `Edit` Metoda vygenerovaná systémem generování uživatelského rozhraní nekontroluje, jestli je ID, které je předáno, platné. Pokud uživatel odebere segment ID z adresy URL ( `http://localhost:xxxxx/Movies/Edit` ), zobrazí se následující chyba:

[![Null_ID](examining-the-edit-methods-and-edit-view/_static/image10.png)](examining-the-edit-methods-and-edit-view/_static/image9.png)

Uživatel může také předat ID, které v databázi neexistuje, například `http://localhost:xxxxx/Movies/Edit/1234` . `HttpGet` `Edit` K vyřešení tohoto omezení můžete provést dvě změny metody Action. Nejprve změňte `ID` parametr tak, aby měl výchozí hodnotu nula, pokud ID není explicitně úspěšné. Můžete také ověřit, že `Find` metoda skutečně našla film před vrácením objektu videa do šablony zobrazení. Aktualizovaná `Edit` Metoda je uvedena níže.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample6.cs)]

Pokud se nenajde žádný film, `HttpNotFound` metoda se zavolá.

Všechny `HttpGet` metody následují podobně jako vzor. Získají filmový objekt (nebo seznam objektů, v případě `Index` ) a předávají model do zobrazení. `Create`Metoda předá prázdný objekt filmu do zobrazení pro vytváření. Všechny metody, které vytvářejí, upravují, odstraňují nebo jinak upravují data, jsou v `HttpPost` přetížení metody. Úprava dat v metodě HTTP GET je bezpečnostní riziko, jak je popsáno v příspěvku na blogu [ASP.NET #46 Tip – nepoužívejte odstranit propojení, protože vytvářejí bezpečnostní otvory](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx). Úpravy dat v metodě GET také porušují osvědčené postupy HTTP a model REST architektury, který určuje, že požadavky GET by neměly měnit stav aplikace. Jinými slovy, provádění operace GET by mělo být bezpečná operace, která nemá žádné vedlejší účinky.

## <a name="adding-a-search-method-and-search-view"></a>Přidání vyhledávací metody a zobrazení vyhledávání

V této části přidáte `SearchIndex` metodu akce, která umožňuje hledat filmy podle žánru nebo názvu. To bude k dispozici pomocí adresy URL */Movies/SearchIndex* . Požadavek zobrazí formulář HTML, který obsahuje vstupní prvky, které může uživatel vyplnit, aby mohl vyhledat film. Když uživatel formulář odešle, metoda Action Získá hodnoty hledání publikované uživatelem a použije hodnoty pro hledání v databázi.

## <a name="displaying-the-searchindex-form"></a>Zobrazení formuláře SearchIndex

Začněte přidáním `SearchIndex` metody akce do existující `MoviesController` třídy. Metoda vrátí zobrazení, které obsahuje formulář HTML. Zde je kód:

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample7.cs)]

První řádek `SearchIndex` metody vytvoří následující dotaz [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) pro výběr filmů:

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample8.cs)]

V tomto okamžiku je definován dotaz, ale ještě nebyl spuštěn v úložišti dat.

Pokud `searchString` parametr obsahuje řetězec, dotaz na filmy je upraven pro filtrování podle hodnoty hledaného řetězce, a to pomocí následujícího kódu:

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample9.cs)]

Dotazy LINQ nejsou provedeny při jejich definování nebo při jejich úpravě voláním metody, jako je `Where` nebo `OrderBy` . Místo toho je provádění dotazu odloženo, což znamená, že vyhodnocení výrazu je zpožděno, dokud se jeho realizovaná hodnota neopakuje nebo je [`ToList`](https://msdn.microsoft.com/library/bb342261.aspx) volána metoda. V `SearchIndex` ukázce je dotaz spuštěn v zobrazení SearchIndex. Další informace o odložení provádění dotazů naleznete v tématu [provádění dotazů](https://msdn.microsoft.com/library/bb738633.aspx).

Nyní můžete implementovat `SearchIndex` zobrazení, které zobrazí formulář uživateli. Klikněte pravým tlačítkem uvnitř `SearchIndex` metody a pak klikněte na **Přidat zobrazení**. V dialogovém okně **Přidat zobrazení** určete, že budete předávat `Movie` objekt šabloně zobrazení jako třídu modelu. V seznamu **šablon generování uživatelského rozhraní** zvolte **seznam**a pak klikněte na **Přidat**.

[![AddSearchView](examining-the-edit-methods-and-edit-view/_static/image12.png)](examining-the-edit-methods-and-edit-view/_static/image11.png)

Po kliknutí na tlačítko **Přidat** se vytvoří šablona zobrazení *Views\Movies\SearchIndex.cshtml* . Vzhledem k tomu, že jste vybrali **seznam** v seznamu **šablon generování uživatelského rozhraní** , aplikace Visual Web Developer automaticky vygenerovala (s generováním uživatelského rozhraní) nějaký výchozí obsah v zobrazení. Generování uživatelského rozhraní vytvořilo formulář HTML. Zkoumala `Movie` třídu a vytvořila kód pro vykreslení `<label>` prvků pro každou vlastnost třídy. Následující výpis zobrazuje zobrazení vytvořit, které bylo vygenerováno:

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample10.cshtml)]

Spusťte aplikaci a přejděte na */Movies/SearchIndex*. Připojit řetězec dotazu, například `?searchString=ghost` k adrese URL. Zobrazí se filtrované filmy.

[![SearchQryStr](examining-the-edit-methods-and-edit-view/_static/image14.png)](examining-the-edit-methods-and-edit-view/_static/image13.png)

Pokud změníte podpis `SearchIndex` metody tak, aby měl parametr s názvem `id` , `id` parametr bude odpovídat `{id}` zástupnému symbolu pro výchozí trasy nastavené v souboru *Global. asax* .

[!code-json[Main](examining-the-edit-methods-and-edit-view/samples/sample11.txt)]

Upravená `SearchIndex` Metoda by vypadala takto:

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample12.cs)]

Nyní můžete název hledání předat jako data trasy (segment adresy URL) místo jako hodnotu řetězce dotazu.

[![SearchRouteData](examining-the-edit-methods-and-edit-view/_static/image16.png)](examining-the-edit-methods-and-edit-view/_static/image15.png)

Nemůžete ale očekávat, že uživatelé můžou upravovat adresu URL pokaždé, když chtějí hledat film. Takže teď přidáte uživatelské rozhraní, které jim umožní filtrovat filmy. Pokud jste změnili podpis `SearchIndex` metody pro testování způsobu předání parametru ID vázaného na trasu, změňte jej tak, aby `SearchIndex` Metoda přebírá řetězcový parametr s názvem `searchString` :

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample13.cs)]

Otevřete soubor *Views\Movies\SearchIndex.cshtml* a hned za `@Html.ActionLink("Create New", "Create")` přidejte následující:

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample14.cshtml)]

Následující příklad ukazuje část souboru *Views\Movies\SearchIndex.cshtml* s přidaným označením filtrování.

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample15.cshtml)]

`Html.BeginForm`Pomocná rutina vytvoří počáteční `<form>` značku. `Html.BeginForm`Pomocná osoba způsobí odeslání formuláře do sebe sama, když ho uživatel odešle kliknutím na tlačítko **Filtr** .

Spusťte aplikaci a zkuste vyhledat film.

[![SearchIndxIE9_title](examining-the-edit-methods-and-edit-view/_static/image18.png)](examining-the-edit-methods-and-edit-view/_static/image17.png)

Neexistuje `HttpPost` přetížení `SearchIndex` metody. Nepotřebujete ho, protože metoda nemění stav aplikace, stačí data filtrovat.

Můžete přidat následující `HttpPost SearchIndex` metodu. V takovém případě by se akce původce shodovala s `HttpPost SearchIndex` metodou a `HttpPost SearchIndex` Metoda by běžela, jak je znázorněno na následujícím obrázku.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample16.cs)]

[![SearchPostGhost](examining-the-edit-methods-and-edit-view/_static/image20.png)](examining-the-edit-methods-and-edit-view/_static/image19.png)

Nicméně i v případě, že přidáte tuto `HttpPost` verzi `SearchIndex` metody, existuje omezení, jak je vše implementováno. Představte si, že chcete vytvořit záložku konkrétního hledání nebo chcete poslat odkaz na přátele, na které můžou kliknout, aby se zobrazil stejný filtrovaný seznam filmů. Všimněte si, že adresa URL požadavku HTTP POST je shodná s adresou URL žádosti GET (localhost: xxxxx/video/SearchIndex) – v samotné adrese URL nejsou žádné vyhledávací informace. Nyní jsou informace o hledaném řetězci odesílány na server jako hodnota pole formuláře. To znamená, že nemůžete zachytit informace o hledání do záložky nebo odeslat přátelům v adrese URL.

Řešením je použití přetížení `BeginForm` , které určuje, že požadavek post by měl přidat informace o hledání do adresy URL a že by měl být směrován do verze HttpGet `SearchIndex` metody. Nahraďte stávající metodu bez parametrů `BeginForm` následujícím způsobem:

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample17.cshtml)]

[![BeginFormPost_SM](examining-the-edit-methods-and-edit-view/_static/image22.png)](examining-the-edit-methods-and-edit-view/_static/image21.png)

Když teď odešlete hledání, adresa URL obsahuje řetězec vyhledávacího dotazu. Hledání bude také jít na `HttpGet SearchIndex` metodu Action, i když máte `HttpPost SearchIndex` metodu.

[![SearchIndexWithGetURL](examining-the-edit-methods-and-edit-view/_static/image24.png)](examining-the-edit-methods-and-edit-view/_static/image23.png)

## <a name="adding-search-by-genre"></a>Přidávání hledání podle žánru

Pokud jste přidali `HttpPost` verzi `SearchIndex` metody, odstraňte ji nyní.

V dalším kroku přidáte funkci, která uživatelům umožní Hledat filmy podle žánru. Nahraďte metodu `SearchIndex` následujícím kódem:

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample18.cs)]

Tato verze `SearchIndex` metody přebírá další parametr, konkrétně `movieGenre` . První pár řádků kódu vytvoří `List` objekt pro uchování filmových žánrů z databáze.

Následující kód je dotaz LINQ, který načte všechny žánry z databáze.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample19.cs)]

Kód používá `AddRange` metodu obecné `List` kolekce k přidání všech různých žánrů do seznamu. (Bez `Distinct` modifikátoru by se přidaly duplicitní žánry – například komedie by se přidalo dvakrát v našem příkladu). Kód pak uloží seznam žánrů v `ViewBag` objektu.

Následující kód ukazuje, jak ověřit `movieGenre` parametr. Pokud není prázdný, kód dál omezí dotaz na filmy, aby se vybrané filmy omezily na zadaný Žánr.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample20.cs)]

## <a name="adding-markup-to-the-searchindex-view-to-support-search-by-genre"></a>Přidání značek do zobrazení SearchIndex pro podporu hledání podle žánru

Přidejte `Html.DropDownList` pomocníka do souboru *Views\Movies\SearchIndex.cshtml* těsně před `TextBox` pomocnou rutinou. Dokončený kód je uveden níže:

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample21.cshtml)]

Spusťte aplikaci a přejděte na */Movies/SearchIndex*. Zkuste hledat podle žánru, podle názvu filmu a podle obou kritérií.

V této části jste prozkoumali metody a pohledy akce CRUD generované rozhraním. Vytvořili jste metodu a zobrazení akce hledání, které umožní uživatelům hledat podle názvu a žánru. V další části se podíváte na postup přidání vlastnosti do `Movie` modelu a postup přidání inicializátoru, který automaticky vytvoří testovací databázi.

> [!div class="step-by-step"]
> [Předchozí](accessing-your-models-data-from-a-controller.md) 
>  [Další](adding-a-new-field.md)
