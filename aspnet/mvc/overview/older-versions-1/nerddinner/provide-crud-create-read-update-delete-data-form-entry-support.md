---
uid: mvc/overview/older-versions-1/nerddinner/provide-crud-create-read-update-delete-data-form-entry-support
title: Poskytnout podporu zadávání datových formulářů CRUD (vytvořit, číst, aktualizovat, odstranit) | Dokumenty společnosti Microsoft
author: rick-anderson
description: Krok 5 ukazuje, jak se naše DinnersController třídy dále povolením podpory pro úpravy, vytváření a odstranění dinners s ním také.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: bbb976e5-6150-4283-a374-c22fbafe29f5
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/provide-crud-create-read-update-delete-data-form-entry-support
msc.type: authoredcontent
ms.openlocfilehash: 2b75a7eda8bce4baa25d92626639f4d904eb363a
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542622"
---
# <a name="provide-crud-create-read-update-delete-data-form-entry-support"></a>Zajištění akcí CRUD (Create, Read, Update, Delete) podporujících zápis dat do formuláře

podle [společnosti Microsoft](https://github.com/microsoft)

[Stáhnout PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Toto je krok 5 zdarma ["NerdDinner" aplikační kurz,](introducing-the-nerddinner-tutorial.md) který prochází, jak vytvořit malé, ale kompletní, webové aplikace pomocí ASP.NET MVC 1.
> 
> Krok 5 ukazuje, jak se naše DinnersController třídy dále povolením podpory pro úpravy, vytváření a odstranění dinners s ním také.
> 
> Pokud používáte ASP.NET MVC 3, doporučujeme postupovat podle kurzů [Začínáme s MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) nebo [MVC Music Store.](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)

## <a name="nerddinner-step-5-create-update-delete-form-scenarios"></a>NerdDinner Krok 5: Vytvořit, aktualizovat, odstranit scénáře formuláře

Zavedli jsme řadiče a zobrazení a zabývali jsme se jejich použitím k implementaci funkce výpisu a podrobností pro večeře na webu. Naším dalším krokem bude, aby naše DinnersController třídy dále a umožnit podporu pro úpravy, vytváření a mazání večeře s ním také.

### <a name="urls-handled-by-dinnerscontroller"></a>Adresy URL zpracovávané ovladačem DinnersController

Dříve jsme přidali metody akce dinnersController, které implementovaly podporu pro dvě adresy URL: */Dinners* and */Dinners/Details/[id]*.

| **Adresa URL** | **Sloveso** | **Účel** |
| --- | --- | --- |
| */Večeře/* | GET | Zobrazení seznamu HTML nadcházejících večeří. |
| */Večeře/Podrobnosti/[id]* | GET | Zobrazit podrobnosti o konkrétní večeři. |

Nyní přidáme metody akce k implementaci tří dalších adres URL: */Dinners/Edit/[id]*, */Dinners/Create*a */Dinners/Delete/[id]*. Tyto adresy URL umožní podporu pro úpravy existující večeře, vytváření nových večeří a odstranění večeří.

Budeme podporovat jak HTTP GET a HTTP POST slovesa interakce s těmito novými adresami URL. Požadavky HTTP GET na tyto adresy URL zobrazí počáteční zobrazení HTML dat (formulář naplněný daty večeři v případě "upravit", prázdný formulář v případě "vytvořit" a obrazovku potvrzení odstranění v případě "odstranit"). HTTP POST požadavky na tyto adresy URL uloží / aktualizovat / odstranit data večeři v našem DinnerRepository (a odtud do databáze).

| **Adresa URL** | **Sloveso** | **Účel** |
| --- | --- | --- |
| */Dinners/Upravit/[id]* | GET | Zobrazí upravitelný formulář HTML naplněný daty večeři. |
| POST | Uložte změny formuláře pro konkrétní večeři do databáze. |
| */Večeře/Vytvořit* | GET | Zobrazí prázdný formulář HTML, který uživatelům umožňuje definovat nové večeře. |
| POST | Vytvořte novou večeři a uložte ji do databáze. |
| */Dinners/Delete/[id]* | GET | Zobrazí potvrzovací obrazovku s mazáním. |
| POST | Odstraní zadanou večeři z databáze. |

### <a name="edit-support"></a>Upravit podporu

Začněme implementací scénáře "upravit".

#### <a name="the-http-get-edit-action-method"></a>Metoda akce úprav protokolu HTTP-GET

Začneme implementací http "GET" chování naší metody upravit akci. Tato metoda bude vyvolána při požadavku na adresu URL */Dinners/Edit/[id].* Naše implementace bude vypadat takto:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample1.cs)]

Výše uvedený kód používá DinnerRepository k načtení Dinner objektu. Potom vykreslí zobrazit šablonu pomocí Dinner objektu. Protože jsme explicitně nepředali název šablony metodě *View(),* použije výchozí cestu založenou na konvencích k vyřešení šablony zobrazení: /Views/Dinners/Edit.aspx.

Nyní vytvoříme tuto šablonu zobrazení. Provedeme to kliknutím pravým tlačítkem myši v rámci metody Edit a výběrem příkazu kontextové nabídky "Přidat zobrazení":

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image1.png)

V dialogovém okně "Přidat zobrazení" označíme, že předáváme objekt Dinner do naší šablony zobrazení jako jeho model, a zvolíme automatické vytvoření uživatelského příkazu šablonu "Upravit":

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image2.png)

Po kliknutí na tlačítko "Přidat" visual studio přidá nový soubor šablony zobrazení "Edit.aspx" pro nás v adresáři "\Views\Dinners". Také otevře novou šablonu zobrazení "Edit.aspx" v editoru kódu - naplněná počáteční implementací uživatelského rozhraní "Upravit", jako je níže:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image3.png)

Pojďme provést několik změn ve výchozím "upravit" generování uživatelského rozhraní a aktualizovat upravit zobrazení šablony mít obsah níže (který odstraní několik vlastností nechceme vystavit):

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample2.aspx)]

Když spustíme aplikaci a požádat *o "/Dinners/Edit/1"* URL uvidíme následující stránku:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image4.png)

Značky HTML generované naším zobrazením vypadají níže. Jedná se o standardní &lt;&gt; HTML – s prvkem formuláře, který provádí HTTP POST na &lt;adresu URL */Dinners/Edit/1* při stisknutí tlačítka "Uložit" vstupní typ="submit"/&gt; . Pro &lt;každou upravitelnou vlastnost&gt; byl výstupem vstupní ho html type="text"// element:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image5.png)

#### <a name="htmlbeginform-and-htmltextbox-html-helper-methods"></a>Html.BeginForm() a Html.TextBox() Html pomocné metody

Naše šablona zobrazení "Edit.aspx" používá několik metod "Html Helper": Html.ValidationSummary(), Html.BeginForm(), Html.TextBox() a Html.ValidationMessage(). Kromě generování značek HTML pro nás tyto pomocné metody poskytují integrovanou podporu zpracování chyb a ověřování.

##### <a name="htmlbeginform-helper-method"></a>Pomocná metoda Html.BeginForm()

Html.BeginForm() pomocná metoda je to, co výstup html &lt;prvek formuláře&gt; v naší značky. V naší šabloně zobrazení Edit.aspx si všimnete, že při použití této metody používáme příkaz C# "using". Otevřená složená závorka označuje začátek obsahu &lt;formuláře&gt; a uzavírací &lt;složená&gt; závorka označuje konec elementu /form:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample3.cs)]

Případně pokud zjistíte, že "using" příkaz přístup nepřirozené pro scénář, jako je tento, můžete použít Html.BeginForm() a Html.EndForm() kombinace (což dělá totéž):

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample4.aspx)]

Volání Html.BeginForm() bez jakýchkoli parametrů způsobí, že výstup elementu formuláře, který provede HTTP-POST na adresu URL aktuálního požadavku. To je důvod, proč naše zobrazení upravit generuje * &lt;prvek form&gt; action="/Dinners/Edit/1" method="post".* Mohli jsme alternativně předalexplicitní parametry Html.BeginForm(), pokud bychom chtěli psát na jinou adresu URL.

##### <a name="htmltextbox-helper-method"></a>Pomocná metoda html.TextBox()

Naše zobrazení Edit.aspx používá pomocnou metodu Html.TextBox() k &lt;&gt; výstupu vstupního typu="text"/ elementů:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample5.aspx)]

Výše uvedená metoda Html.TextBox() přebírá jeden parametr – který se používá k &lt;určení atributů id/name vstupního parametru type="text"/&gt; pro výstup, stejně jako vlastnost modelu k naplnění hodnoty textového pole. Například objekt Dinner, který jsme předali zobrazení Pro úpravy, měl hodnotu vlastnosti "Title" ".NET Futures", a tak naše metoda Html.TextBox("Title") metoda volání výstup: * &lt;input id="Title" name="Title" type="text" value=".NET Futures" /&gt;*.

Alternativně můžeme použít první Parametr Html.TextBox() k určení id/název prvku a pak explicitně předat hodnotu použít jako druhý parametr:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample6.aspx)]

Často budeme chtít provést vlastní formátování na hodnotu, která je výstupem. Pro tyto scénáře je užitečná statická metoda String.Format() vestavěná do rozhraní .NET. Naše šablona zobrazení Edit.aspx používá tuto hodnotu EventDate (která je typu DateTime) tak, aby se na čas nezobrazovala sekundy:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample7.aspx)]

Třetí parametr html.textbox() lze volitelně použít k vytvoření dalších atributů HTML. Fragment kódu níže ukazuje, jak vykreslit atribut additional size="30" a atribut class="mycssclass" na vstupním &lt;type="text"/&gt; elementu. Všimněte si, jak jsme unikající název@" character because "atributu třídy pomocí "class" je vyhrazené klíčové slovo v C#:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample8.aspx)]

#### <a name="implementing-the-http-post-edit-action-method"></a>Implementace metody akce úprav protokolu HTTP-POST

Nyní máme implementovanou http-get verzi naší metody akce úprav. Když uživatel požádá o adresu *URL /Dinners/Edit/1,* obdrží stránku HTML takto:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image6.png)

Stisknutí tlačítka "Uložit" způsobí, že příspěvek formuláře na adresu URL */Dinners/Edit/1* a odešle hodnoty vstupního &lt;&gt; formuláře HTML pomocí slovesa HTTP POST. Nyní implementujeme chování HTTP POST naší metody upravit akci – která bude zpracovávat ukládání Večeři.

Začneme přidáním přetížené metody akce "Upravit" do našeho DinnersController, který má atribut AcceptVerbs, který označuje, že zpracovává scénáře HTTP POST:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample9.cs)]

Pokud je atribut [AcceptVerbs] použit na přetížené metody akce, ASP.NET MVC automaticky zpracovává odesílání požadavků na příslušnou metodu akce v závislosti na příchozím slovese HTTP. Požadavky HTTP POST na adresy URL */Dinners/Edit/[id]* přejdou na výše uvedenou metodu úprav, zatímco všechny ostatní požadavky http slovesa na adresy URL */Dinners/Edit/[id]* přejdou na první metodu úprav, kterou jsme implementovali (která neměla `[AcceptVerbs]` atribut).

| **Boční téma: Proč rozlišovat pomocí HTTP sloves?** |
| --- |
| Můžete se zeptat - proč používáme jednu adresu URL a rozlišujeme její chování pomocí slovesa HTTP? Proč nemít jen dvě samostatné adresy URL pro zpracování načítání a ukládání změn úprav? Příklad: /Dinners/Edit/[id] pro zobrazení počátečního formuláře a /Dinners/Save/[id] pro zpracování příspěvku formuláře k jeho uložení? Nevýhodou publikování dvou samostatných adres URL je, že v případech, kdy jsme psát na /Dinners/Save/2, a pak je třeba znovu zobrazit formulář HTML z důvodu vstupní chyby, koncový uživatel skončí s /Dinners/Save/2 URL v adresním řádku svého prohlížeče (protože to byla adresa URL formulář zaúčtovaný). Pokud koncový uživatel záložky této redisplayed stránky do svého seznamu oblíbených položek prohlížeče, nebo zkopíruje / vloží ADRESU URL a e-maily s přítelem, budou nakonec ukládání URL, která nebude fungovat v budoucnu (protože tato adresa URL závisí na post hodnoty). Vystavením jedné adresy URL (například: /Dinners/Edit/[id]) a diferenciací zpracování pomocí slovesa HTTP je pro koncové uživatele bezpečné záložku upravit stránku a/nebo odeslat adresu URL ostatním. |

#### <a name="retrieving-form-post-values"></a>Načítání hodnot příspěvku formuláře

Existuje celá řada způsobů, jak můžeme přistupovat k parametrům zaúčtovaných formulářů v rámci naší metody HTTP POST "Edit". Jeden jednoduchý přístup je stačí použít Request vlastnost na controller základní třídy pro přístup k kolekci formuláře a načíst zaúčtované hodnoty přímo:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample10.cs)]

Výše uvedený přístup je trochu podrobný, i když, zejména poté, co přidáme logiku zpracování chyb.

Lepší mů e pro tento scénář je využít integrované *UpdateModel()* pomocné metody na controller základní třídy. Podporuje aktualizaci vlastností objektu, který předáváme pomocí parametrů příchozího formuláře. Používá reflexe k určení názvů vlastností v objektu a pak automaticky převede a přiřadí jim hodnoty na základě vstupních hodnot odeslaných klientem.

Mohli bychom použít UpdateModel() metoda pro zjednodušení naší HTTP-POST Upravit akci pomocí tohoto kódu:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample11.cs)]

Nyní můžeme navštívit adresu URL */Dinners/Edit/1* a změnit název naší večeře:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image7.png)

Když klikneme na tlačítko "Uložit", provedeme formulářový příspěvek do naší akce Upravit a aktualizované hodnoty budou v databázi zachovány. Poté budeme přesměrováni na adresu URL podrobností pro večeři (která zobrazí nově uložené hodnoty):

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image8.png)

#### <a name="handling-edit-errors"></a>Zpracování chyb při úpravách

Naše současná implementace HTTP-POST funguje dobře – s výjimkou případů, kdy se jedná o chyby.

Když uživatel provede chybu při úpravách formuláře, musíme se ujistit, že je formulář znovu zobrazen s informativní chybovou zprávou, která je vede k jeho opravě. To zahrnuje případy, kdy koncový uživatel zaúčtuje nesprávný vstup (například: poškozený řetězec data), stejně jako případy, kdy je vstupní formát platný, ale dochází k porušení obchodního pravidla. Pokud dojde k chybám, formulář by měl zachovat vstupní data, která uživatel původně zadal, aby nemusel své změny doplňovat ručně. Tento proces by se měl opakovat tolikrát, kolikrát je to nutné, dokud se formulář úspěšně nedokončí.

ASP.NET MVC obsahuje některé pěkné vestavěné funkce, které usnadňují manipulaci s chybami a opětovné zobrazení formulářů. Chcete-li tyto funkce zobrazit v akci, aktualizujte naši metodu akce úpravy pomocí následujícího kódu:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample12.cs)]

Výše uvedený kód je podobný naší předchozí implementaci – kromě toho, že jsme nyní balení try/catch chyba zpracování bloku kolem naší práce. Pokud dojde k výjimce při volání UpdateModel(), nebo při pokusu o uložení DinnerRepository (což vyvolá výjimku, pokud Dinner objekt, který se pokoušíme uložit, je neplatný z důvodu porušení pravidla v rámci našeho modelu), bude spuštěn náš blok zpracování chyb catch. V rámci jsme smyčky přes všechna porušení pravidel, které existují v Dinner objektu a přidat je do ModelState objektu (které budeme diskutovat v nejbližší době). Poté znovu zobrazíme pohled.

Chcete-li vidět tuto práci, spusťme aplikaci znovu, upravte večeři a změňte ji tak, aby měla prázdný název, datum události "BOGUS" a použijte telefonní číslo uk s hodnotou země USA. Když stiskneme tlačítko "Uložit", naše metoda úpravy HTTP POST nebude moci uložit večeři (protože tam jsou chyby) a znovu zobrazí formulář:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image9.png)

Naše aplikace má slušnou chybovou zkušenost. Textové prvky s neplatným vstupem jsou zvýrazněny červeně a chybové zprávy ověření jsou zobrazeny koncovému uživateli o nich. Formulář také zachovává vstupní data, která uživatel původně zadal , aby nemusel nic doplňovat.

Jak, můžete se zeptat, k tomu došlo? Jak se textová pole Název, Datum události a ContactPhone zvýrazňují červeně a vědí, že mají vykázat původně zadané uživatelské hodnoty? A jak se chybové zprávy dostaly do seznamu v horní části? Dobrou zprávou je, že k tomu nedošlo kouzlem - spíše to bylo proto, že jsme použili některé z vestavěných funkcí ASP.NET MVC, které usnadňují ověření vstupu a zpracování chyb.

#### <a name="understanding-modelstate-and-the-validation-html-helper-methods"></a>Principy modelového stavu a ověřovacích metod nápovědy HTML

Třídy kontroleru mají kolekci vlastností "ModelState", která poskytuje způsob, jak označit, že existují chyby s objektem modelu předávaným zobrazení. Chybové položky v kolekci ModelState identifikují název vlastnosti modelu s problémem (například:"Název", "EventDate" nebo "ContactPhone") a povolit, aby byla zadána chybová zpráva šetrná k uživateli (například: "Název je povinný").

*UpdateModel()* pomocná metoda automaticky naplní ModelState kolekce při výskytu chyb při pokusu o přiřazení hodnoty formuláře vlastností na objekt modelu. Například naše Vlastnost EventDate objektu Dinner je typu DateTime. Když UpdateModel() metoda nebyla schopna přiřadit hodnotu řetězce "BOGUS" k němu ve výše uvedeném scénáři, UpdateModel() metoda přidána položka do ModelState kolekce označující chybu přiřazení došlo s této vlastnosti.

Vývojáři mohou také napsat kód explicitně přidat položky chyb do kolekce ModelState, jako děláme níže v rámci našeho bloku zpracování chyb "catch", který je vyplnění ModelState kolekce s položkami na základě aktivní porušení pravidel v Dinner objektu:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample13.cs)]

#### <a name="html-helper-integration-with-modelstate"></a>Integrace pomocníka Html s ModelState

Pomocné metody HTML - jako Html.TextBox() - zkontrolujte kolekci ModelState při vykreslování výstupu. Pokud pro položku existuje chyba, vykreslují hodnotu zadanou uživatelem a třídu chyb CSS.

Například v našem zobrazení "Upravit" používáme pomocnou metodu Html.TextBox() k vykreslení EventDate našeho objektu Dinner:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample14.aspx)]

Při zobrazení byla vykreslena v chybovém scénáři, Html.TextBox() metoda zkontrolovat ModelState kolekce, zda byly nějaké chyby spojené s "EventDate" vlastnost naše Dinner objektu. Když zjistil, že došlo k chybě, vykreslil odeslaný uživatelský vstup ("BOGUS") jako &lt;hodnotu a přidal třídu chyby css do vstupního typu ="textové pole"/&gt; značky, které generoval:

[!code-html[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample15.html)]

Můžete přizpůsobit vzhled css error class vypadat však chcete. Výchozí třída chyb css – "input-validation-error" – je definována ve stylu *\content\site.css* a vypadá takto:

[!code-css[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample16.css)]

Toto pravidlo CSS je to, co způsobilo, že naše neplatné vstupní prvky byly zvýrazněny jako níže:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image10.png)

##### <a name="htmlvalidationmessage-helper-method"></a>Html.ValidationMessage() Pomocná metoda

Pomocná metoda Html.ValidationMessage() lze použít k výstupu chybové zprávy ModelState přidružené k určité vlastnosti modelu:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample17.aspx)]

Výše uvedené výstupy kódu: * &lt;span&gt; class="field-validation-error" Hodnota&lt;"BOGUS" je neplatná /span&gt;*

Pomocná metoda Html.ValidationMessage() také podporuje druhý parametr, který umožňuje vývojářům přepsat chybovou textovou zprávu, která je zobrazena:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample18.aspx)]

Výše uvedené výstupy kódu: * &lt;span&gt;\*&lt;class="field-validation-error" /span&gt; * namísto výchozího textu chyby, když je pro vlastnost EventDate přítomna chyba.

##### <a name="htmlvalidationsummary-helper-method"></a>Pomocná metoda Html.ValidationSummary()

Pomocná metoda Html.ValidationSummary() lze použít k vykreslení souhrnné chybové zprávy, doprovázené &lt;seznamem všech&gt;&lt;&gt;&lt;&gt; podrobných chybových zpráv v kolekci ModelState:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image11.png)

Pomocná metoda Html.ValidationSummary() přebírá volitelný parametr řetězce , který definuje souhrnnou chybovou zprávu, která se zobrazí nad seznamem podrobných chyb:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample19.aspx)]

Volitelně můžete použít CSS přepsat, co seznam chyb vypadá.

#### <a name="using-a-addruleviolations-helper-method"></a>Použití pomocné metody AddRuleViolations

Naše počáteční http-post upravit implementace používá foreach prohlášení v rámci jeho catch bloku smyčku přes porušení pravidel objektu Večeři a přidat je do kolekce ModelState řadiče:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample20.cs)]

Můžeme tento kód trochu čistší přidáním třídy "ControllerHelpers" do projektu NerdDinner a implementovat metodu rozšíření "AddRuleViolations" v rámci ní, která přidá pomocnou metodu do třídy ASP.NET MVC ModelStateDictionary. Tato metoda rozšíření můžete zapouzdřit logiku potřebnou k naplnění ModelStateDictionary se seznamem chyb RuleViolation:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample21.cs)]

Můžeme pak aktualizovat naši metodu akce úpravy HTTP-POST, abychom použili tuto metodu rozšíření k naplnění kolekce ModelState s našimi porušeními pravidel večeři.

#### <a name="complete-edit-action-method-implementations"></a>Kompletní implementace metod upravit akci

Níže uvedený kód implementuje všechny logiky řadiče nezbytné pro náš scénář upravit:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample22.cs)]

Pěkná věc na naší implementaci úprav je, že ani naše třída Controller, ani naše šablona view nemusí vědět nic o konkrétním ověření nebo obchodních pravidlech vynucených naším modelem večeři. Můžeme přidat další pravidla pro náš model v budoucnu a nemusí provádět žádné změny kódu na náš řadič nebo zobrazení, aby byly podporovány. To nám poskytuje flexibilitu snadno vyvíjet naše požadavky na aplikace v budoucnu s minimálními změnami kódu.

### <a name="create-support"></a>Vytvořit podporu

Dokončili jsme implementaci chování "Upravit" naší DinnersController třídy. Pojďme nyní přesunout na implementaci "Vytvořit" podporu na něm - což umožní uživatelům přidávat nové večeře.

#### <a name="the-http-get-create-action-method"></a>Metoda akce create HTTP-GET

Začneme implementací http "GET" chování naší metody vytvořit akci. Tato metoda bude volána, když někdo navštíví *adresu URL /Dinners/Create.* Naše implementace vypadá takto:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample23.cs)]

Výše uvedený kód vytvoří nový Objekt Dinner a přiřadí jeho EventDate vlastnost být jeden týden v budoucnosti. Potom vykreslí Zobrazení, který je založen na nový Objekt Dinner. Vzhledem k tomu, že jsme explicitně nepředali název metodě pomocníka *View(),* použije výchozí cestu založenou na konvencích k vyřešení šablony zobrazení: /Views/Dinners/Create.aspx.

Nyní vytvoříme tuto šablonu zobrazení. Můžeme to udělat kliknutím pravým tlačítkem myši v rámci metody Vytvořit akci a výběrem příkazu kontextové nabídky "Přidat zobrazení". V dialogovém okně "Přidat zobrazení" označíme, že předáváme objekt Dinner šabloně zobrazení, a zvolíme automatické vytváření uživatelského okna šablony "Vytvořit":

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image12.png)

Po kliknutí na tlačítko "Přidat" visual studio uloží nové zobrazení "Create.aspx" založené na lešení do adresáře "\Views\Dinners" a otevře ho v rámci rozhraní IDE:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image13.png)

Pojďme udělat několik změn ve výchozím "vytvořit" generování souboru, který byl vygenerován pro nás, a upravit jej tak, aby vypadal jako níže:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample24.aspx)]

A teď, když spustíme naši aplikaci a přístup *k "/Dinners/Create"* URL v prohlížeči bude vykreslovat ui jako níže z naší implementace vytvořit akci:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image14.png)

#### <a name="implementing-the-http-post-create-action-method"></a>Implementace metody vytvoření akce HTTP-POST

Máme implementovanou http-get verzi naší metody akce Vytvořit. Když uživatel klepne na tlačítko "Uložit", provede příspěvek formuláře na adresu URL */Dinners/Create* a odešle hodnoty vstupního &lt;&gt; formuláře HTML pomocí slovesa HTTP POST.

Nyní implementujeme chování HTTP POST naší metody akce create. Začneme přidáním přetížené metody akce "Vytvořit" do našeho DinnersController, který má atribut AcceptVerbs, který označuje, že zpracovává scénáře HTTP POST:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample25.cs)]

Existuje celá řada způsobů, jak můžeme přistupovat k parametrům zaúčtovaného formuláře v rámci naší metody "Vytvořit" s podporou HTTP-POST.

Jedním z přístupů je vytvoření nového objektu Dinner a potom pomocí pomocné metody *UpdateModel()* (jako jsme to udělali s akcí Úpravy) k jeho naplnění zaúčtované hodnotami formuláře. Můžeme jej pak přidat do našeho DinnerRepository, zachovat do databáze a přesměrovat uživatele na naše podrobnosti akce zobrazit nově vytvořené Večeři pomocí kódu níže:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample26.cs)]

Alternativně můžeme použít přístup, kde máme naše Create() metoda akce trvat Dinner objekt jako parametr metody. ASP.NET MVC pak automaticky vytvoří konkretizovat nový objekt Dinner, naplní jeho vlastnosti pomocí vstupů formuláře a předá jej naší metodě akce:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample27.cs)]

Naše metoda akce výše ověří, že Objekt Dinner byl úspěšně naplněn hodnotami příspěvku formuláře kontrolou vlastnosti ModelState.IsValid. To vrátí false, pokud existují problémy vstupní převod (například řetězec "BOGUS" pro EventDate vlastnost), a pokud existují nějaké problémy naše metoda akce znovu zobrazí formulář.

Pokud vstupní hodnoty jsou platné, pak metoda akce se pokusí přidat a uložit nové Dinner do DinnerRepository. Zalomí tuto práci v rámci try/catch bloku a znovu zobrazí formulář, pokud existují jakékoli porušení obchodnípravidla (což by způsobilo dinnerRepository.Save() metoda vyvolat výjimku).

Chcete-li zobrazit tuto chybu zpracování chování v akci, můžeme požádat */Dinners/Create* URL a vyplnit podrobnosti o nové večeři. Nesprávný vstup nebo hodnoty způsobí, že formulář vytvořit bude znovu zobrazen s chybami zvýrazněnými jako níže:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image15.png)

Všimněte si, jak náš formulář Vytvořit respektuje přesně stejná pravidla ověření a obchodní pravidla jako náš formulář pro úpravy. Důvodem je, že naše ověření a obchodní pravidla byly definovány v modelu a nebyly vloženy do ui nebo kontroleru aplikace. To znamená, že můžeme později změnit/ vyvíjet naše validace nebo obchodní pravidla na jednom místě a nechat je použít v celé naší aplikaci. Nebudeme muset měnit žádný kód v rámci našich upravit nebo vytvořit akční metody automaticky respektovat nová pravidla nebo změny stávajících.

Když opravíme vstupní hodnoty a znovu klikneme na tlačítko "Uložit", náš přírůstek do DinnerRepository bude úspěšný a do databáze bude přidána nová večeře. Poté budeme přesměrováni na adresu URL */Dinners/Details/[id]* – kde nám budou představeny podrobnosti o nově vytvořené večeři:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image16.png)

### <a name="delete-support"></a>Odstranit podporu

Pojďme nyní přidat "Odstranit" podporu našedinnersController.

#### <a name="the-http-get-delete-action-method"></a>Metoda akce odstranění HTTP-GET

Začneme implementací http get chování naší metody akce delete. Tato metoda bude volat, když někdo navštíví *adresu URL /Dinners/Delete/[id].* Níže je implementace:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample28.cs)]

Metoda akce se pokusí načíst Večeři, která má být odstraněna. Pokud Dinner existuje vykreslí Zobrazení na základě Dinner objektu. Pokud objekt neexistuje (nebo již byl odstraněn), vrátí zobrazení, které vykreslí šablonu zobrazení "NotFound", kterou jsme vytvořili dříve pro naši metodu akce Podrobnosti.

Šablonu zobrazení "Odstranit" můžeme vytvořit kliknutím pravým tlačítkem myši v rámci metody akce Delete a výběrem příkazu kontextové nabídky "Přidat zobrazení". V dialogovém okně "Přidat zobrazení" označíme, že předáváme objekt Dinner do naší šablony zobrazení jako jeho model a zvolíme vytvoření prázdné šablony:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image17.png)

Po kliknutí na tlačítko "Přidat" visual studio přidá nový soubor šablony zobrazení Delete.aspx pro nás v našem adresáři "\Views\Dinners". Do šablony přidáme nějaký KÓD HTML a kód, abychom implementovali potvrzovací obrazovku pro odstranění, jako je níže:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample29.aspx)]

Výše uvedený kód zobrazí název večeři, která má &lt;&gt; být odstraněna a výstupy prvek formuláře, který provede POST na adresu URL /Dinners/Delete/[id], pokud koncový uživatel klepne na tlačítko "Odstranit" v něm.

Když spustíme naši aplikaci a přístup *k "/Dinners/Delete/[id]"* URL pro platný objekt Dinner vykreslí ui jako níže:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image18.png)

| **Boční téma: Proč děláme POST?** |
| --- |
| Můžete se zeptat - proč jsme prošli &lt;&gt; úsilím o vytvoření formuláře v rámci naší obrazovky potvrzení odstranit? Proč nepoužít standardní hypertextový odkaz k propojení s metodou akce, která provádí skutečnou operaci odstranění? Důvodem je, že chceme být opatrní, abychom se ochránili před webovými prohledávači a vyhledávači, kteří objevili naše adresy URL a neúmyslně způsobili, že data budou odstraněna, když sledují odkazy. Adresy URL založené na PROTOKOLU HTTP-GET jsou považovány za "bezpečné" pro přístup/procházení a mají nesledovat adresy HTTP-POST. Dobrým pravidlem je, abyste se ujistili, že vždy vložíte destruktivní operace nebo operace úpravy dat za požadavky HTTP-POST. |

#### <a name="implementing-the-http-post-delete-action-method"></a>Implementace metody akce odstranění protokolu HTTP-POST

Nyní máme http-get verzi naší metody akce Delete implementována, která zobrazuje odstranit potvrzení obrazovky. Když koncový uživatel klikne na tlačítko "Odstranit", provede příspěvek formuláře na adresu URL */Dinners/Dinner/[id].*

Nyní implementujeme http "POST" chování metody akce delete pomocí následujícího kódu:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample30.cs)]

Http-POST verze naší Delete akce metoda pokusí načíst objekt večeři odstranit. Pokud ji nemůže najít (protože již byla odstraněna), vykreslí naši šablonu "NotFound". Pokud najde Dinner, odstraní z DinnerRepository. Poté vykreslí šablonu "Odstraněno".

Chcete-li implementovat šablonu "Odstraněno", klikneme pravým tlačítkem myši na metodu akce a zvolíme kontextovou nabídku "Přidat zobrazení". Pojmenujeme naše zobrazení "Odstraněno" a budeme ji mít jako prázdnou šablonu (a nebudeme mít objekt modelu silného typu). Poté do něj přidáme nějaký obsah HTML:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample31.aspx)]

A teď, když spustíme naši aplikaci a přístup *k "/Dinners/Delete/[id]"* URL pro platný objekt Dinner bude vykreslovat naše večeře odstranit potvrzení obrazovky jako níže:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image19.png)

Když klikneme na tlačítko "Odstranit", provede adresu URL HTTP-POST na *adresu /Dinners/Delete/[id],* která odstraní večeři z naší databáze a zobrazí naši šablonu zobrazení "Smazané":

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image20.png)

### <a name="model-binding-security"></a>Zabezpečení vazby modelu

Probrali jsme dva různé způsoby použití vestavěných funkcí vazby modelu ASP.NET MVC. První pomocí UpdateModel() metoda aktualizovat vlastnosti na existující objekt modelu a druhý pomocí ASP.NET mvc podporu pro předávání objektů modelu jako parametry metody akce. Obě tyto techniky jsou velmi silné a velmi užitečné.

Tato moc s sebou také nese odpovědnost. Je důležité být vždy paranoidní o zabezpečení při přijímání všech vstupů uživatele, a to platí také při vazby objekty formulář vstup. Měli byste být opatrní vždy HTML kódovat všechny uživatelem zadané hodnoty, aby se zabránilo html a JavaScript injektáž útoky, a dávejte pozor na útoky injektáže SQL (poznámka: používáme LINQ na SQL pro naši aplikaci, která automaticky kóduje parametry, aby se zabránilo tyto typy útoků). Nikdy byste se neměli spoléhat pouze na ověření na straně klienta a vždy používat ověření na straně serveru, abyste se ochránili před hackery, kteří se pokoušejí odeslat falešné hodnoty.

Jedna další položka zabezpečení, ujistěte se, že přemýšlíte o při použití funkce vazby ASP.NET MVC je rozsah objektů, které jsou závazné. Konkrétně chcete, abyste se ujistili, že rozumíte důsledkům zabezpečení vlastností, které umožňují být vázány, a ujistěte se, že povolíte pouze ty vlastnosti, které by měly být aktualizovatelné koncovým uživatelem, které mají být aktualizovány.

Ve výchozím nastavení se metoda UpdateModel() pokusí aktualizovat všechny vlastnosti objektu modelu, které odpovídají hodnotám parametrů příchozího formuláře. Podobně objekty předané jako parametry metody akce také ve výchozím nastavení mohou mít všechny své vlastnosti nastaveny pomocí parametrů formuláře.

#### <a name="locking-down-binding-on-a-per-usage-basis"></a>Uzamčení vazby na základě použití

Zásady vazby můžete uzamknout na základě použití poskytnutím explicitní "zahrnout seznam" vlastností, které lze aktualizovat. To lze provést předáním parametru pole další řetězec updatemodel() jako níže:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample32.cs)]

Objekty předané jako parametry metody akce také podporují atribut [Bind], který umožňuje zadat "zahrnout seznam" povolených vlastností jako níže:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample33.cs)]

#### <a name="locking-down-binding-on-a-type-basis"></a>Uzamčení vazby na základě typu

Můžete také uzamknout pravidla vazby na základě typu. To umožňuje zadat pravidla vazby jednou a pak je použít ve všech scénářích (včetně scénáře UpdateModel a parametr metody akce) napříč všemi řadiči a metodami akce.

Pravidla vazby podle typu můžete přizpůsobit přidáním atributu [Bind] k typu nebo jeho registrací v souboru Global.asax aplikace (užitečné pro scénáře, kde typ nevlastníte). Potom můžete použít Bind atribut u include a exclude vlastnosti řídit, které vlastnosti jsou vazby pro konkrétní třídy nebo rozhraní.

Použijeme tento postup pro Dinner třídy v naší aplikaci NerdDinner a přidat [Bind] atribut, který omezuje seznam vazebných vlastností na následující:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample34.cs)]

Všimněte si, že nepovolujeme, aby byla kolekce RSVPs manipulována prostřednictvím vazby, ani nepovolujeme vlastnosti DinnerID nebo HostedBy, které mají být nastaveny prostřednictvím vazby. Z bezpečnostních důvodů budeme místo toho pouze manipulovat s těmito konkrétními vlastnostmi pomocí explicitního kódu v rámci našich metod akce.

### <a name="crud-wrap-up"></a>CRUD Wrap-Up

ASP.NET MVC obsahuje řadu předdefinovaných funkcí, které pomáhají s implementací scénáře účtování formulářů. Použili jsme celou řadu těchto funkcí poskytovat podporu ui CRUD na vrcholu našedinnerRepository.

K implementaci naší aplikace používáme přístup zaměřený na model. To znamená, že všechny naše logiky ověřování a obchodnípravidla jsou definovány v rámci vrstvy modelu – a nikoli v rámci našich řadičů nebo zobrazení. Naše třída Controller ani naše šablony zobrazení nevědí nic o konkrétních obchodních pravidlech vynucených naší třídou modelu Dinner.

To udrží naši architekturu aplikací čistou a usnadní testování. Můžeme přidat další obchodní pravidla do naší vrstvy modelu v budoucnu a *není třeba provádět žádné změny kódu* našeho řadiče nebo zobrazení, aby byly podporovány. To nám poskytne velkou flexibilitu, abychom se v budoucnu vyvíjeli a měnili naši aplikaci.

Naše DinnersController nyní umožňuje večeře výpisy /podrobnosti, stejně jako vytvořit, upravit a odstranit podporu. Kompletní kód pro třídu naleznete níže:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample35.cs)]

### <a name="next-step"></a>Další krok

Nyní máme základní CRUD (Vytvořit, Číst, Aktualizovat a odstranit) podporu implementovat v rámci naší DinnersController třídy.

Podívejme se nyní na to, jak můžeme použít ViewData a ViewModel třídy povolit ještě bohatší uI na našich formulářích.

> [!div class="step-by-step"]
> [Předchozí](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
> [další](use-viewdata-and-implement-viewmodel-classes.md)
