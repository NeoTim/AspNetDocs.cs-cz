---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/form-basics
title: Představujeme ASP.NET webových stránek - Základy formulářů HTML | Dokumenty společnosti Microsoft
author: Rick-Anderson
description: Tento kurz ukazuje základy, jak vytvořit vstupní formulář a jak zpracovat vstup uživatele při použití ASP.NET webových stránek (Razor). A teď, když...
ms.author: riande
ms.date: 05/28/2015
ms.assetid: 81ed82bf-b940-44f1-b94a-555d0cb7cc98
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/form-basics
msc.type: authoredcontent
ms.openlocfilehash: f57661077ec3bb13f3d4ec41b130bda4d2fb9070
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676326"
---
# <a name="introducing-aspnet-web-pages---html-form-basics"></a>Představujeme ASP.NET webových stránek - Základy formulářů HTML

, autor: [Tom FitzMacken](https://github.com/tfitzmac)

> Tento kurz ukazuje základy, jak vytvořit vstupní formulář a jak zpracovat vstup uživatele při použití ASP.NET webových stránek (Razor). A teď, když máte databázi, budete používat své dovednosti formuláře, aby uživatelé našli konkrétní filmy v databázi. Předpokládá, že jste dokončili sérii prostřednictvím [úvodu k zobrazení dat pomocí ASP.NET webových stránek](/aspnet/web-pages/overview/getting-started/introducing-aspnet-web-pages-2/displaying-data).
> 
> Naučíte se:
> 
> - Jak vytvořit formulář pomocí standardních prvků HTML.
> - Jak číst vstup uživatele ve formuláři.
> - Jak vytvořit dotaz SQL, který selektivně získává data pomocí hledaného výrazu, který uživatel poskytuje.
> - Jak mít pole na stránce "pamatovat", co uživatel zadal.
>   
> 
> Funkce / technologie diskutovány:
> 
> - Objekt `Request`
> - Klauzule `Where` SQL.

## <a name="what-youll-build"></a>Co budete stavět

V předchozím kurzu jste vytvořili databázi, přidali do `WebGrid` ní data a potom pomocí pomocníka k zobrazení dat. V tomto kurzu přidáte vyhledávací pole, které vám umožní najít filmy určitého žánru nebo jehož název obsahuje jakékoli slovo, které zadáte. (Například budete moci najít všechny filmy, jejichž žánr je "Akce" nebo jejichž název obsahuje "Harry" nebo "Dobrodružství.")

Až budete hotovi s tímto kurzem, budete mít stránku, jako je tato:

![Stránka Filmy s hledáním žánru a nadpisu](form-basics/_static/image1.png)

Výpis část stránky je stejný jako v &mdash; posledním kurzu mřížky. Rozdíl bude v tom, že mřížka bude zobrazovat pouze filmy, které jste hledali.

## <a name="about-html-forms"></a>O formulářích HTML

(Pokud máte zkušenosti s vytvářením formulářů HTML `GET` `POST`a s rozdílem mezi a , můžete tuto část přeskočit.)

Formulář obsahuje textová &mdash; pole uživatelských vstupních prvků, tlačítka, přepínací tlačítka, zaškrtávací políčka, rozevírací seznamy a tak dále. Uživatelé vyplní tyto ovládací prvky nebo prodají výběr a poté odešlou formulář klepnutím na tlačítko.

Základní syntaxe formuláře HTML je ilustrována v tomto příkladu:

[!code-html[Main](form-basics/samples/sample1.html)]

Když se tato značka spustí na stránce, vytvoří jednoduchý formulář, který vypadá jako tento obrázek:

![Základní formulář HTML vykreslený v prohlížeči](form-basics/_static/image2.png)

Prvek `<form>` uzavře prvky HTML, které mají být odeslány. (Snadná chyba, aby se je přidat prvky na stránku, ale pak zapomenout dát je uvnitř `<form>` prvku. V takovém případě není nic předloženo.) Atribut `method` informuje prohlížeč, jak odeslat vstup uživatele. Tuto možnost `post` nastavíte na pokud provádíte aktualizaci `get` na serveru nebo pokud právě načítáte data ze serveru.

<a id="GET,_POST,_and_HTTP_Verb_Safety"></a>

> [!TIP] 
> 
> **Bezpečnost sloves GET, POST a HTTP**
> 
> HTTP, protokol, který prohlížeče a servery používají k výměně informací, je pozoruhodně jednoduchý ve svých základních operacích. Prohlížeče používají pouze několik sloves k požadavkům na servery. Při psaní kódu pro web je užitečné pochopit tato slovesa a způsob, jakým je prohlížeč a server používají. Zdaleka nejčastěji používaná slovesa jsou tato:
> 
> - `GET`. Prohlížeč používá toto sloveso k načtení něco ze serveru. Například při zadání adresy URL do prohlížeče prohlížeč `GET` provede operaci, která požaduje požadovanou stránku. Pokud stránka obsahuje grafiku, `GET` prohlížeč provede další operace získat obrázky. Pokud `GET` má operace předat informace na server, informace jsou předány jako součást adresy URL v řetězci dotazu.
> - `POST`. Prohlížeč odešle `POST` požadavek na odeslání dat, která mají být přidána nebo změněna na serveru. Sloveso `POST` se například používá k vytvoření záznamů v databázi nebo ke změně existujících záznamů. Většinu času, když vyplníte formulář a kliknete na `POST` tlačítko odeslat, prohlížeč provede operaci. V `POST` operaci data předávaná serveru je v těle stránky.
> 
> Důležitým rozdílem mezi těmito `GET` slovesy je, že operace nemá nic měnit na serveru – nebo `GET` ji umístit trochu abstraktnějším způsobem, operace nevede ke změně stavu na serveru. Můžete provést `GET` operaci se stejnými prostředky tolikrát, kolikrát chcete, a tyto prostředky se nezmění. (Operace `GET` je často řekl, aby byl "bezpečný", nebo použít technický termín, je *idempotentní*.) Naproti tomu požadavek `POST` změní něco na serveru při každém provedení operace.
> 
> Tento rozdíl pomohou dva příklady. Když provádíte vyhledávání pomocí motoru, jako je Bing nebo Google, vyplníte formulář, který se skládá z jednoho textového pole, a potom kliknete na tlačítko vyhledávání. Prohlížeč provede `GET` operaci s hodnotou, kterou jste zadali do pole předané jako součást adresy URL. Použití `GET` operace pro tento typ formuláře je v pořádku, protože vyhledávací operace nezmění žádné prostředky na serveru, pouze načte informace.
> 
> Nyní zvažte proces objednání něčeho online. Vyplníte podrobnosti objednávky a kliknete na tlačítko Odeslat. Tato operace bude `POST` požadavek, protože operace bude mít za následek změny na serveru, jako je například nový záznam objednávky, změna informací o účtu a možná mnoho dalších změn. Na `GET` rozdíl od operace `POST` nelze požadavek opakovat – pokud ano, pokaždé, když jste žádost znovu odeslali, vygenerovali byste na serveru novou objednávku. (V takových případech vás weby často varují, abyste neklikali na tlačítko odeslat více než jednou, nebo zakáže tlačítko odeslat, abyste formulář omylem neodeslali znovu.)
> 
> V průběhu tohoto kurzu budete používat `GET` operaci i `POST` operaci pro práci s formuláři HTML. V každém případě vysvětlíme, proč je sloveso, které používáte, vhodné.
> 
> (Další informace o slovesech PROTOKOLU HTTP naleznete v článku [Definice metod](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html) na webu W3C.)

Většina uživatelských `<input>` vstupních prvků jsou elementy HTML. Vypadají jako `<input type="type" name="name">,` kde *typ* označuje druh uživatelského ovládacího prvku, který chcete. Tyto prvky jsou běžné:

- Textové pole:`<input type="text">`
- Políčko:`<input type="check">`
- Přepínač:`<input type="radio">`
- Tlačítko:`<input type="button">`
- Tlačítko Odeslat:`<input type="submit">`

Prvek můžete také `<textarea>` použít k vytvoření víceřádkového textového `<select>` pole a prvek k vytvoření rozevíracího seznamu nebo posuvného seznamu. (Další informace o prvcích formuláře HTML naleznete v [tématu Html Forms and Input](http://www.w3schools.com/html/html_forms.asp) on the W3Schools site.)

Atribut `name` je velmi důležité, protože název je, jak budete získat hodnotu prvku později, jak uvidíte v brzké době.

Zajímavá část je to, co vy, vývojář stránky, dělat se vstupem uživatele. Neexistuje žádné předdefinované chování spojené s těmito prvky. Místo toho musíte získat hodnoty, které uživatel zadal nebo vybral, a provést s nimi něco. To je to, co se naučíte v tomto tutoriálu.

> [!TIP] 
> 
> **HTML5 a vstupní formuláře**
> 
> Jak možná víte, HTML je v přechodu a nejnovější verze (HTML5) obsahuje podporu pro intuitivnější způsoby, jak mohou uživatelé zadávat informace. Například v HTML5 můžete (vývojář stránky) sdělit stránce, že chcete, aby uživatel zadá datum. Prohlížeč pak může automaticky zobrazit kalendář, nikoli vyžadovat, aby uživatel zadá datum ručně. HTML5 je však nový a ještě není podporován ve všech prohlížečích.
> 
> ASP.NET webových stránek podporuje vstup HTML5 v rozsahu, v jakém to dělá prohlížeč uživatele. Představu o nových atributech `<input>` prvku v HTML5 najdete v tématu Atribut [vstupního &lt;&gt; typu HTML](http://www.w3schools.com/html/html_form_input_types.asp) na webu W3Schools.

## <a name="creating-the-form"></a>Vytvoření formuláře

V aplikaci WebMatrix otevřete v pracovním prostoru **Soubory** stránku *Movies.cshtml.*

Za uzavírací `</h1>` značku a `<div>` před `grid.GetHtml` otevírací značku hovoru přidejte následující značky:

[!code-html[Main](form-basics/samples/sample2.html)]

Tato značka vytvoří formulář s názvem `searchGenre` textového pole a tlačítkem odeslat. Textové pole a tlačítko odeslat `<form>` jsou `method` uzavřeny v `get`prvku, jehož atribut je nastaven na . (Nezapomeňte, že pokud nevložíte textové pole a `<form>` tlačítko odeslat do prvku, nic se po kliknutí na tlačítko neodešle.) Zde používáte `GET` sloveso, protože vytváříte formulář, který na serveru neprovádí žádné změny – pouze výsledkem je hledání. (V předchozím kurzu jste `post` použili metodu, která je způsob odeslání změn na server. Uvidíte, že v příštím kurzu znovu.)

Spusťte stránku. Přestože jste pro formulář nedefinovali žádné chování, můžete vidět, jak vypadá:

![Stránka Filmy s vyhledávacím polem pro Žánr](form-basics/_static/image3.png)

Zadejte hodnotu do textového pole, například Komedie. Potom klepněte na **položku Žánr hledání**.

Poznamenejte si adresu URL stránky. Protože jste `<form>` nastavili `method` atribut `get`prvku na , hodnota, kterou jste zadali, je nyní součástí řetězce dotazu v adrese URL, například takto:

`http://localhost:45661/Movies.cshtml?searchGenre=Comedy`

## <a name="reading-form-values"></a>Čtení hodnot formuláře

Stránka již obsahuje nějaký kód, který získá data databáze a zobrazí výsledky v mřížce. Nyní musíte přidat nějaký kód, který čte hodnotu textového pole, takže můžete spustit dotaz SQL, který obsahuje hledaný termín.

Vzhledem k tomu, že `get`jste nastavili metodu formuláře na , můžete hodnotu, která byla zadána do textového pole, přečíst pomocí následujícího kódu:

`var searchTerm = Request.QueryString["searchGenre"];`

Objekt `Request.QueryString` `QueryString` (vlastnost objektu) `Request` obsahuje hodnoty prvků, které byly odeslány jako součást `GET` operace. Vlastnost `Request.QueryString` obsahuje *kolekci* (seznam) hodnot, které jsou odeslány ve formuláři. Chcete-li získat libovolnou jednotlivou hodnotu, zadejte název požadovaného prvku. To je důvod, proč `name` musíte mít `<input>` atribut`searchTerm`na prvek ( ), který vytváří textové pole. (Další informace `Request` o objektu naleznete na [postranním panelu](#BKMK_TheRequestObject) později.)

Je to dost jednoduché číst hodnotu textového pole. Pokud však uživatel do textového pole vůbec nic nezadal, ale přesto kliknul na **Tlačítko Hledat,** můžete toto kliknutí ignorovat, protože není co hledat.

Následující kód je příklad, který ukazuje, jak implementovat tyto podmínky. (Tento kód ještě nemusíte přidávat; za chvíli to uděláte.)

[!code-csharp[Main](form-basics/samples/sample3.cs)]

Test se porouchá tímto způsobem:

- Získejte hodnotu `Request.QueryString["searchGenre"]`, konkrétně hodnotu, `<input>` která `searchGenre`byla zadána do prvku s názvem .
- Zjistěte, zda je prázdný `IsEmpty` pomocí metody. Tato metoda je standardní způsob, jak zjistit, zda něco (například prvek formuláře) obsahuje hodnotu. Ale opravdu, záleží vám pouze v případě, že *to není* prázdné, proto ...
- Přidejte `!` operátor před `IsEmpty` zkoušku. (Operátor `!` znamená logické NOT).

V jednoduché angličtině `if` se celá podmínka překládá do následujícího: *Pokud je vyhledávací prvek formulářegenre prázdný, pak ...*

Tento blok nastaví půdu pro vytvoření dotazu, který používá hledaný výraz. Uděláte to v další části.

<a id="BKMK_TheRequestObject"></a>

> [!TIP] 
> 
> **Objekt požadavku**
> 
> Objekt `Request` obsahuje všechny informace, které prohlížeč odešle do vaší aplikace, když je stránka požadována nebo odeslána. Tento objekt obsahuje všechny informace, které uživatel poskytne, jako jsou hodnoty textového pole nebo soubor k nahrání. Obsahuje také všechny druhy dalších informací, jako jsou soubory cookie, hodnoty v řetězci dotazu URL (pokud existuje), cesta k souboru stránky, která je spuštěna, typ prohlížeče, který uživatel používá, seznam jazyků, které jsou nastaveny v prohlížeči, a mnoho dalšího.
> 
> Objekt `Request` je *kolekce* (seznam) hodnot. Získáte individuální hodnotu z kolekce zadáním jeho název:
> 
> `var someValue = Request["name"];`
> 
> Objekt `Request` ve skutečnosti zveřejňuje několik podsad. Příklad:
> 
> - `Request.Form`poskytuje hodnoty z prvků `<form>` uvnitř odeslaného prvku, pokud je požadavek požadavek. `POST`
> - `Request.QueryString`poskytuje pouze hodnoty v řetězci dotazu adresy URL. (V adrese `http://mysite/myapp/page?searchGenre=action&page=2`URL, `?searchGenre=action&page=2` jako je , je část adresy URL řetězec dotazu.)
> - `Request.Cookies`umožňuje přístup k souborům cookie, které prohlížeč odeslal.
> 
> Chcete-li získat hodnotu, o které víte, `Request["name"]`že je v odeslané podobě, můžete použít . Případně můžete použít konkrétnější verze `Request.Form["name"]` (pro `POST` požadavky) nebo `Request.QueryString["name"]` (pro `GET` požadavky). Samozřejmě, *název* je název položky získat.
> 
> Název položky, kterou chcete získat, musí být jedinečný v rámci kolekce, kterou používáte. To je důvod, `Request` proč objekt `Request.Form` poskytuje `Request.QueryString`podmnožiny jako a . Předpokládejme, že vaše stránka `userName` obsahuje prvek formuláře `userName`s názvem a *také* soubor cookie s názvem . Pokud se `Request["userName"]`dostanete , je nejednoznačné, zda chcete hodnotu formuláře nebo soubor cookie. Pokud však `Request.Form["userName"]` získáte `Request.Cookie["userName"]`nebo , jste explicitní o tom, jakou hodnotu získat.
> 
> Je vhodné být konkrétní a používat `Request` podmnožinu, která vás zajímá, jako `Request.Form` nebo `Request.QueryString`. Pro jednoduché stránky, které vytváříte v tomto kurzu, to pravděpodobně není opravdu žádný rozdíl. Při vytváření složitějších stránek však pomocí `Request.Form` `Request.QueryString` explicitní verze nebo můžete zabránit problémům, které mohou nastat, když stránka obsahuje formulář (nebo více formulářů), soubory cookie, hodnoty řetězců dotazů a tak dále.

## <a name="creating-a-query-by-using-a-search-term"></a>Vytvoření dotazu pomocí hledaného termínu

Nyní, když víte, jak získat hledaný výraz, který uživatel zadal, můžete vytvořit dotaz, který jej používá. Nezapomeňte, že chcete-li získat všechny položky filmu z databáze, používáte dotaz SQL, který vypadá jako tento příkaz:

`SELECT * FROM Movies`

Chcete-li získat pouze určité filmy, musíte `Where` použít dotaz, který obsahuje klauzuli. Tato klauzule umožňuje nastavit podmínku, na které jsou vráceny řádky dotazem. Tady je příklad:

`SELECT * FROM Movies WHERE Genre = 'Action'`

Základním formátem `WHERE column = value`je . Můžete použít různé operátory `=` `>` kromě jen `<` , jako `<>` (větší než), `<=` (menší než), (nerovná se), (menší než nebo rovno), atd., v závislosti na tom, co hledáte.

V případě, že vás to zajímá, &mdash; `SELECT` příkazy `Select` SQL nejsou `select`rozlišování malých a velkých písmen je stejný jako (nebo dokonce ). Lidé však často velká slova v příkazu `SELECT` `WHERE`SQL, jako a , aby bylo snazší číst.

### <a name="passing-the-search-term-as-a-parameter"></a>Předání hledaného výrazu jako parametru

Hledání určitého žánru je`WHERE Genre = 'Action'`snadné ( ), ale chcete mít možnost vyhledat libovolný žánr, který uživatel zadá. Chcete-li to provést, můžete vytvořit jako dotaz SQL, který obsahuje zástupný symbol pro hodnotu hledat. Bude vypadat jako tento příkaz:

`SELECT * FROM Movies WHERE Genre = @0`

Zástupný symbol `@` je znak následovaný nulou. Jak můžete hádat, dotaz může obsahovat více zástupných `@0`symbolů a budou pojmenovány , `@1`, `@2`atd.

Chcete-li nastavit dotaz a skutečně předat hodnotu, použijte kód jako následující:

[!code-sql[Main](form-basics/samples/sample4.sql)]

Tento kód je podobný tomu, co jste již udělali pro zobrazení dat v mřížce. Jedinými rozdíly jsou:

- Dotaz obsahuje zástupný`WHERE Genre = @0"`symbol ( ).
- Dotaz je vložen do`selectCommand`proměnné ( ); předtím, jste předaldotaz přímo `db.Query` metodě.
- Při volání `db.Query` metody předáte dotaz i hodnotu, která se má použít pro zástupný symbol. (Pokud dotaz měl více zástupných symbolů, předejte je všechny jako samostatné hodnoty metodě.)

Pokud dáte všechny tyto prvky dohromady, získáte následující kód:

[!code-csharp[Main](form-basics/samples/sample5.cs)]

> [!NOTE] 
> 
> **Důležité!** Použití zástupných `@0`symbolů (například) k předání hodnot příkazu SQL je *velmi důležité* pro zabezpečení. Způsob, jakým vidíte zde, se zástupnými symboly pro proměnná data, je jediný způsob, jak byste měli vytvořit příkazy SQL.
> 
> Nikdy sestavit příkaz SQL tím, že dohromady (zřetězení) literál text a hodnoty, které dostanete od uživatele. Zřetězení vstupu uživatele do příkazu SQL otevře váš web k *útoku injektáží SQL,* kde uživatel se zlými úmysly odešle na vaši stránku hodnoty, které hacknou vaši databázi. (Další informace naleznete v článku [SQL Injection](https://msdn.microsoft.com/library/ms161953.aspx) na webu MSDN.)

## <a name="updating-the-movies-page-with-search-code"></a>Aktualizace stránky Filmy pomocí vyhledávacího kódu

Nyní můžete aktualizovat kód v souboru *Movies.cshtml.* Chcete-li začít, nahraďte kód v bloku kódu v horní části stránky tímto kódem:

[!code-csharp[Main](form-basics/samples/sample6.cs)]

Rozdíl je v tom, že jste `selectCommand` dotaz vložili do proměnné, do které předáte `db.Query` později. Uvedení příkazu SQL do proměnné umožňuje změnit příkaz, což je co provedete pro provedení hledání.

Také jste odstranili tyto dva řádky, které budete dát zpět později:

[!code-csharp[Main](form-basics/samples/sample7.cs)]

Ještě nechcete spustit dotaz (tj. volání) `db.Query`a nechcete ani inicializovat `WebGrid` pomocníka. Budete dělat ty věci poté, co jste zjistili, který příkaz SQL má spustit.

Po tomto přepsaném bloku můžete přidat novou logiku pro zpracování hledání. Vyplněný kód bude vypadat takto. Aktualizujte kód na stránce tak, aby odpovídal tomuto příkladu:

[!code-cshtml[Main](form-basics/samples/sample8.cshtml)]

Stránka nyní funguje takto. Při každém spuštění stránky kód otevře databázi a `selectCommand` proměnná je nastavena na `Movies` příkaz SQL, který získá všechny záznamy z tabulky. Kód také inicializuje `searchTerm` proměnnou.

Pokud však aktuální požadavek obsahuje `searchGenre` hodnotu prvku, kód se nastaví `selectCommand` na jiný `Where` dotaz – konkrétně na ten, který obsahuje klauzuli k hledání žánru. To také `searchTerm` nastaví na to, co bylo předáno pro vyhledávací pole (což může být nic).

Bez ohledu na to, `selectCommand`který příkaz `db.Query` SQL je v , kód `searchTerm`pak volá ke spuštění dotazu, předání matné, co je v . Pokud není nic `searchTerm`v , na tom nezáleží, protože v takovém případě neexistuje `selectCommand` žádný parametr předat hodnotu tak jako tak.

Nakonec kód inicializuje `WebGrid` pomocníka pomocí výsledků dotazu, stejně jako předtím.

Můžete vidět, že vložením příkazu SQL a hledaného výrazu do proměnných, jste přidali flexibilitu kódu. Jak uvidíte dále v tomto kurzu, můžete použít tento základní rámec a pokračovat v přidávání logiky pro různé typy vyhledávání.

## <a name="testing-the-search-by-genre-feature"></a>Testování funkce Vyhledávání podle žánru

Ve službě WebMatrix spusťte stránku *Movies.cshtml.* Zobrazí se stránka s textovým polem pro žánr.

Zadejte žánr, který jste zadali pro jeden z testovacích záznamů, a klikněte na **Hledat**. Tentokrát vidíte seznam pouze filmů, které odpovídají tomuto žánru:

![Filmy výpis stránky po hledání žánru 'Komedie'](form-basics/_static/image4.png)

Zadejte jiný žánr a znovu vyhledejte. Zkuste zadat žánr pomocí všech malých nebo velkých písmen, abyste viděli, že hledání nerozlišuje malá a velká písmena.

## <a name="remembering-what-the-user-entered"></a>"Zapamatování" Co uživatel zadal

Možná jste si všimli, že po zadání žánru a kliknutí na **položku Žánr vyhledávání**jste viděli výpis pro daný žánr. Jinými slovy však &mdash; bylo vyhledávací textové pole prázdné, nepamatovalo si, co jste zadali.

Je důležité pochopit, proč k tomuto chování dochází. Při odeslání stránky prohlížeč odešle požadavek na webový server. Když ASP.NET dostane požadavek, vytvoří zcela novou instanci stránky, spustí v něm kód a pak znovu vykreslí stránku do prohlížeče. Ve skutečnosti však stránka neví, že jste právě pracovali s předchozí verzí sebe sama. Vše, co ví, je, že dostal požadavek, který měl nějaké formuláře dat v něm.

Pokaždé, když požádáte o stránku, &mdash; ať už &mdash; poprvé nebo odesláním, získáte novou stránku. Webový server nemá paměť na poslední požadavek. Ani ASP.NET, a ani prohlížeč. Jediné spojení mezi těmito samostatnými instancemi stránky jsou všechna data, která mezi nimi přenášíte. Pokud například odešlete stránku, může nová instance stránky získat data formuláře, která byla odeslána předchozí instancí. (Dalším způsobem, jak předávat data mezi stránkami, je používání souborů cookie.)

Formální způsob, jak popsat tuto situaci, je říci, že webové stránky jsou *bez státní příslušnosti*. Webové servery a samotné stránky a prvky na stránce neudržují žádné informace o předchozím stavu stránky. Web byl navržen tak, protože udržování stavu pro jednotlivé požadavky by rychle vyčerpalo zdroje webových serverů, které často zpracovávají tisíce, možná i stovky tisíc požadavků za sekundu.

Proto bylo textové pole prázdné. Po odeslání stránky ASP.NET vytvořilnovou instanci stránky a prošel kódem a značkami. V tom kódu nebylo nic, co by ASP.NET řeklo, aby do textového pole vložili hodnotu. Takže ASP.NET nic neudělala a textové pole bylo vykresleno bez hodnoty.

Je tu vlastně snadný způsob, jak obejít tento problém. Žánr, který jste zadali *is* do textového &mdash; pole, je `Request.QueryString["searchGenre"]`k dispozici v kódu, který je v .

Aktualizujte značky pro textové pole `value` tak, aby `searchTerm`atribut získá jeho hodnotu z , jako v tomto příkladu:

[!code-html[Main](form-basics/samples/sample9.html?highlight=1)]

Na této stránce můžete také `value` nastavit atribut `searchTerm` proměnné, protože tato proměnná také obsahuje zadaný žánr. Ale pomocí `Request` objektu `value` nastavit atribut, jak je znázorněno zde je standardní způsob, jak provést tento úkol. (Za předpokladu, že &mdash; to chcete udělat i v některých situacích, můžete chtít vykreslit stránku *bez* hodnot v polích. Vše závisí na tom, co se děje s vaší aplikací.)

> [!NOTE]
> Nemůžete si "zapamatovat" hodnotu textového pole, které se používá pro hesla. Bylo by bezpečnostní díru, která by lidem umožnila vyplnit pole s heslem pomocí kódu.

Spusťte stránku znovu, zadejte žánr a klepněte na **položku Žánr hledání**. Tentokrát nejen že vidíte výsledky hledání, ale textové pole si pamatuje, co jste zadali naposledy:

![Stránka zobrazující, že textové pole si "zapamatovalo" předchozí položku](form-basics/_static/image5.png)

## <a name="searching-for-any-word-in-the-title"></a>Hledání libovolného slova v názvu

Nyní můžete vyhledat libovolný žánr, ale můžete také vyhledat název. Při hledání je těžké získat přesně správný název, takže místo toho můžete vyhledat slovo, které se objeví kdekoli uvnitř názvu. Chcete-li to provést v `LIKE` SQL, použijte operátor a syntaxi takto:

`SELECT * FROM Movies WHERE Title LIKE '%adventure%'`

Tento příkaz získá všechny filmy, jejichž názvy obsahují "dobrodružství". Při použití `LIKE` operátoru zahrnete `%` zástupný znak jako součást hledaného výrazu. Hledání `LIKE 'adventure%'` znamená "začíná na 'dobrodružství'". (Technicky to znamená "Řetězec 'dobrodružství' následovaný ničím.") Podobně hledaný výraz `LIKE '%adventure'` znamená "cokoliv následované řetězcem "dobrodružství", což je další způsob, jak říci "končící na "dobrodružství".

Hledaný `LIKE '%adventure%'` výraz proto znamená "s 'dobrodružství' kdekoli v názvu." (Technicky, "cokoliv v názvu, následuje 'dobrodružství', následuje cokoliv.")

Uvnitř `<form>` prvku přidejte následující značky přímo `</div>` pod uzavírací značku pro `</form>` vyhledávání žánru (těsně před uzavírací prvek):

[!code-html[Main](form-basics/samples/sample10.html)]

Kód pro zpracování tohoto hledání je podobný kódu pro vyhledávání žánru, `LIKE` s tím rozdílem, že budete muset sestavit hledání. Uvnitř bloku kódu v horní části stránky `if` přidejte `if` tento blok těsně za blok pro vyhledávání žánru:

[!code-csharp[Main](form-basics/samples/sample11.cs)]

Tento kód používá stejnou logiku, kterou jste `LIKE` viděli dříve, s`%`tím rozdílem, že hledání používá operátor a kód umístí " " před a za hledaný termín.

Všimněte si, jak bylo snadné přidat další vyhledávání na stránku. Stačilo jen:

- Vytvořte `if` blok, který testoval, abyste zjistili, zda příslušné vyhledávací pole má hodnotu.
- Nastavte `selectCommand` proměnnou na nový příkaz SQL.
- Nastavte `searchTerm` proměnnou na hodnotu, která má být předávána dotazu.

Zde je kompletní blok kódu, který obsahuje novou logiku pro vyhledávání titulů:

[!code-cshtml[Main](form-basics/samples/sample12.cshtml)]

Zde je přehled toho, co tento kód dělá:

- Proměnné `searchTerm` a `selectCommand` jsou inicializovány v horní části. Nastavíte tyto proměnné na příslušný hledaný výraz (pokud existuje) a příslušný příkaz SQL na základě toho, co uživatel dělá na stránce. Výchozí hledání je jednoduchý případ získání všech filmů z databáze.
- V testech `searchGenre` `searchTitle`pro a `searchTerm` , kód nastaví na hodnotu, kterou chcete vyhledat. Tyto bloky kódu `selectCommand` také nastavit na příslušný příkaz SQL pro toto hledání.
- Metoda `db.Query` je vyvolána pouze jednou, pomocí `selectedCommand` libovolného příkazu `searchTerm`SQL je v a bez ohledu na hodnotu je v . Pokud neexistuje žádný vyhledávací dotaz (žádný žánr a `searchTerm` žádné titulní slovo), hodnota je prázdný řetězec. Na tom však nezáleží, protože v takovém případě dotaz nevyžaduje parametr.

## <a name="testing-the-title-search-feature"></a>Testování funkce vyhledávání v názvu

Nyní můžete otestovat dokončenou vyhledávací stránku. Spusťte *Movies.cshtml*.

Zadejte žánr a klepněte na **položku Žánr vyhledávání**. Mřížka zobrazuje filmy tohoto žánru, stejně jako předtím.

Zadejte titulní slovo a klepněte na **položku Název hledání**. Mřížka zobrazuje filmy, které mají toto slovo v názvu.

![Filmy výpis stránky po vyhledání 'The' v názvu](form-basics/_static/image6.png)

Ponechte obě textová pole prázdná a klepněte na jedno z těchto tlačítek. Mřížka zobrazuje všechny filmy.

## <a name="combining-the-queries"></a>Kombinování dotazů

Můžete si všimnout, že vyhledávání, která můžete provádět, jsou výhradní. Název a žánr nelze prohledávat současně, a to ani v případě, že v obou vyhledávacích polích jsou hodnoty. Nemůžete například vyhledat všechny akční filmy, jejichž název obsahuje "Dobrodružství". (Vzhledem k tomu, že stránka je nyní kódována, pokud zadáte hodnoty pro žánr i název, získá přednost hledání nadpisu.) Chcete-li vytvořit hledání, které kombinuje podmínky, budete muset vytvořit dotaz SQL, který má syntaxi, jako je následující:

`SELECT * FROM Movies WHERE Genre = @0 AND Title LIKE @1`

A budete muset spustit dotaz pomocí příkazu, jako je následující (zhruba řečeno):

`var selectedData = db.Query(selectCommand, searchGenre, searchTitle);`

Vytvoření logiky, která umožní mnoho permutací vyhledávacích kritérií, se může trochu zapojit, jak můžete vidět. Proto tady zastavíme.

## <a name="coming-up-next"></a>Již brzy

V dalším kurzu vytvoříte stránku, která pomocí formuláře umožní uživatelům přidávat filmy do databáze.

## <a name="complete-listing-for-movie-page-updated-with-search"></a>Kompletní výpis pro film ovou stránku (aktualizováno pomocí vyhledávání)

[!code-cshtml[Main](form-basics/samples/sample13.cshtml)]

## <a name="additional-resources"></a>Další zdroje

- [Úvod do ASP.NET webovéprogramování pomocí syntaxe břitvy](https://go.microsoft.com/fwlink/?LinkID=202890)
- [SQL KDE klauzule](http://www.w3schools.com/sql/sql_where.asp) na webu W3Schools
- [Článek definice metody](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html) na webu W3C

> [!div class="step-by-step"]
> [Předchozí](displaying-data.md)
> [další](entering-data.md)
