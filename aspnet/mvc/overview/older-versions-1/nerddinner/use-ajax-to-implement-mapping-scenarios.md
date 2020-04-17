---
uid: mvc/overview/older-versions-1/nerddinner/use-ajax-to-implement-mapping-scenarios
title: Použití nástroje AJAX k implementaci scénářů mapování | Dokumenty společnosti Microsoft
author: rick-anderson
description: Krok 11 ukazuje, jak integrovat podporu mapování AJAX do naší aplikace NerdDinner, což umožňuje uživatelům, kteří vytvářejí, upravují nebo sledují večeře, aby viděli l...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: f731990a-0a81-4d62-81df-87d676cdedd6
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-ajax-to-implement-mapping-scenarios
msc.type: authoredcontent
ms.openlocfilehash: f2e2640eb421d5ee8006915f46cbe1090b8d21ad
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542583"
---
# <a name="use-ajax-to-implement-mapping-scenarios"></a>Použití jazyka AJAX k implementaci scénářů mapování

podle [společnosti Microsoft](https://github.com/microsoft)

[Stáhnout PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Toto je krok 11 zdarma ["NerdDinner" aplikační kurz,](introducing-the-nerddinner-tutorial.md) který prochází, jak vytvořit malé, ale kompletní, webové aplikace pomocí ASP.NET MVC 1.
> 
> Krok 11 ukazuje, jak integrovat podporu mapování AJAX do naší aplikace NerdDinner, což umožňuje uživatelům, kteří vytvářejí, upravují nebo zobrazují večeře, graficky zobrazit umístění večeře.
> 
> Pokud používáte ASP.NET MVC 3, doporučujeme postupovat podle kurzů [Začínáme s MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) nebo [MVC Music Store.](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)

## <a name="nerddinner-step-11-integrating-an-ajax-map"></a>NerdDinner Krok 11: Integrace AJAX mapa

Nyní uděláme naši aplikaci trochu vizuálně vzrušující integrací podpory mapování AJAX. To umožní uživatelům, kteří vytvářejí, upravují nebo prohlížejí večeře, aby graficky viděli umístění večeře.

### <a name="creating-a-map-partial-view"></a>Vytvoření částečného zobrazení mapy

Budeme používat funkce mapování na několika místech v rámci naší aplikace. Chcete-li zachovat náš kód SUCHÝ budeme zapouzdřit společné funkce mapy v rámci jedné částečné šablony, které můžeme znovu použít napříč více akce mise a zobrazení. Pojmenujeme toto částečné zobrazení "map.ascx" a vytvoříme jej v adresáři \Views\Dinners.

Můžeme vytvořit map.ascx částečné kliknutím pravým tlačítkem myši na \Views\Dinners adresáře a výběrem Add-&gt;View příkaz menu. Pojmenujeme zobrazení "Map.ascx", zkontrolujeme jej jako částečný pohled a označíme, že mu předáme modelovou třídu "Večeře":

![](use-ajax-to-implement-mapping-scenarios/_static/image1.png)

Po kliknutí na tlačítko "Přidat" bude vytvořena naše částečná šablona. Poté aktualizujeme soubor Map.ascx tak, aby měl následující obsah:

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample1.aspx)]

První &lt;odkaz&gt; na skript odkazuje na knihovnu mapování Microsoft Virtual Earth 6.2. Druhý &lt;&gt; skript odkaz odkazuje na soubor map.js, který budeme brzy vytvořit, který bude zapouzdřit naše společné Javascript mapování logiku. Div &lt;id="theMap"&gt; element je kontejner HTML, který virtuální země bude používat k hostování mapy.

Pak máme vložený &lt;&gt; blok skriptu, který obsahuje dvě funkce JavaScriptu specifické pro toto zobrazení. První funkce používá jQuery k drátu funkce, která se spustí, když je stránka připravena ke spuštění skriptu na straně klienta. Volá LoadMap() pomocná funkce, kterou budeme definovat v rámci našeho souboru skriptu Map.js načíst virtuální kontrolu mapy Země. Druhá funkce je obslužná rutina události zpětného volání, která přidá pin do mapy, který identifikuje umístění.

Všimněte si, jak používáme blok&gt; %= % na straně &lt;serveru v bloku skriptu na straně klienta k vložení zeměpisné šířky a délky večeře, kterou chceme namapovat do JavaScriptu. Jedná se o užitečnou techniku pro výstup dynamických hodnot, které lze použít skriptem na straně klienta (bez nutnosti samostatného volání AJAX zpět na server k načtení hodnot – což je rychlejší). Bloky &lt;%=&gt; % se spustí při vykreslování zobrazení na serveru – a výstup HTML tak skončí s vloženými hodnotami JavaScriptu (například: var latitude = 47.64312;).

### <a name="creating-a-mapjs-utility-library"></a>Vytvoření knihovny nástrojů Map.js

Pojďme nyní vytvořit soubor Map.js, který můžeme použít k zapouzdření funkce JavaScriptpro naši mapu (a implementovat LoadMap a LoadPin metody výše). Můžeme to udělat kliknutím pravým tlačítkem myši na adresář \Scripts v&gt;rámci našeho projektu a poté zvolte příkaz nabídky "Přidat novou položku", vyberte položku Jazyka JScript a pojmenujte ji "Map.js".

Níže je javascriptový kód přidáme do souboru Map.js, který bude komunikovat s Virtual Earth pro zobrazení naší mapy a přidat umístění kolíky k němu pro naše večeře:

[!code-javascript[Main](use-ajax-to-implement-mapping-scenarios/samples/sample2.js)]

### <a name="integrating-the-map-with-create-and-edit-forms"></a>Integrace mapy s vytvářením a úpravami formulářů

Nyní integrujeme podporu mapy s našimi stávajícími scénáři vytváření a úprav. Dobrou zprávou je, že je to docela snadné-do, a nevyžaduje, abychom změnit některý z našich kód řadiče. Vzhledem k tomu, že naše vytvořit a upravit zobrazení sdílet společné "DinnerForm" částečné zobrazení k implementaci formuláře večeři ui, můžeme přidat mapu na jednom místě a mají obě naše vytvořit a upravit scénáře použít.

Vše, co potřebujeme, je otevřít částečné zobrazení \Views\Dinners\DinnerForm.ascx a aktualizovat jej tak, aby zahrnoval naši novou mapu částečnou. Níže je, co aktualizované DinnerForm bude vypadat, jakmile je přidána mapa (poznámka: HTML prvky formuláře jsou vynechány z kódu fragment níže pro stručnost):

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample3.aspx)]

DinnerForm částečné výše trvá objekt typu "DinnerFormViewModel" jako jeho typ modelu (protože potřebuje jak Dinner objekt, stejně jako SelectList naplnit rozevírací seznam zemí). Naše mapa částečné potřebuje pouze objekt typu "Večeře" jako jeho typ modelu, a tak když jsme vykreslit mapu částečné jsme předávání jen Večeři sub-vlastnost DinnerFormViewModel na to:

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample4.aspx)]

Funkce JavaScriptu, kterou jsme přidali k částečnému, používá jQuery k připojení události "rozostření" do textového pole HTML "Adresa". Pravděpodobně jste slyšeli o událostech "zaostření", které se spálí, když uživatel klikne nebo zapíše karty do textového pole. Opak je "rozostření" událost, která se spustí, když uživatel ukončí textové pole. Výše uvedená obslužná rutina události vymaže hodnoty textového pole zeměpisné šířky a délky, když k tomu dojde, a potom vykreslí nové umístění adresy na naší mapě. Obslužná rutina události zpětného volání, kterou jsme definovali v souboru map.js, pak aktualizuje textová pole zeměpisné délky a šířky v našem formuláři pomocí hodnot vrácených virtuální zemí na základě adresy, kterou jsme jí dali.

A teď, když jsme se spustit naši aplikaci znovu a klikněte na záložku "Host Večeře" uvidíme výchozí mapu zobrazí spolu s našimi standardními prvky formuláře Večeře:

![](use-ajax-to-implement-mapping-scenarios/_static/image2.png)

Když zadáme adresu a potom kartu pryč, mapa se dynamicky aktualizuje, aby se zobrazilo umístění, a naše obslužná rutina události naplní textová pole zeměpisné šířky a délky hodnotami umístění:

![](use-ajax-to-implement-mapping-scenarios/_static/image3.png)

Pokud uložíme novou večeři a znovu ji otevřeme pro úpravy, zjistíme, že umístění mapy se zobrazí při načtení stránky:

![](use-ajax-to-implement-mapping-scenarios/_static/image4.png)

Při každé změně pole adresy se aktualizuje mapa a souřadnice zeměpisné šířky a délky.

Nyní, když mapa zobrazuje umístění večeře, můžeme také změnit pole formuláře Zeměpisná šířka a zeměpisná délka z viditelných textových polí na skryté prvky (protože mapa je automaticky aktualizuje při každém zadání adresy). Chcete-li to provést, přejdeme z pomocníka HTML.TextBox() HTML na pomocnou metodu Html.Hidden():

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample5.aspx)]

A teď naše formuláře jsou trochu uživatelsky přívětivější a vyhnout se zobrazení surové zeměpisné šířky / délky (zatímco ještě jejich ukládání s každou večeři v databázi):

![](use-ajax-to-implement-mapping-scenarios/_static/image5.png)

### <a name="integrating-the-map-with-the-details-view"></a>Integrace mapy se zobrazením podrobností

Teď, když máme mapu integrovanou s našimi scénáři vytváření a úprav, integrujeme ji také s naším scénářem Podrobnosti. Vše, co potřebujeme, je &lt;zavolat % Html.RenderPartial("mapa"); %&gt; v zobrazení Podrobnosti.

Níže je uvedeno, jak vypadá zdrojový kód do úplného zobrazení Podrobnosti (s mapovou integrací):

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample6.aspx)]

A teď, když uživatel přejde na / Večeře / Podrobnosti / [id] URL uvidí podrobnosti o večeři, umístění večeře na mapě (kompletní s push-pin, že když se vznášel nad zobrazí název večeře a adresu), a mají AJAX odkaz na RSVP pro to:

![](use-ajax-to-implement-mapping-scenarios/_static/image6.png)

### <a name="implementing-location-search-in-our-database-and-repository"></a>Implementace vyhledávání polohy v naší databázi a úložišti

Chcete-li dokončit naši implementaci AJAX, přidejte mapu na domovskou stránku aplikace, která umožňuje uživatelům graficky vyhledávat večeře v jejich blízkosti.

![](use-ajax-to-implement-mapping-scenarios/_static/image7.png)

Začneme implementací podpory v rámci naší vrstvy databáze a úložiště dat, abychom mohli efektivně provádět vyhledávání v poloměru založené na poloze pro dinners. Mohli bychom použít nové [geoprostorové funkce SQL 2008](https://www.microsoft.com/sqlserver/2008/en/us/spatial-data.aspx) k implementaci tohoto, nebo alternativně můžeme použít [http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx](http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx) funkci SQL přístup, který Gary Dryden diskutovali v článku zde: a Rob Conery blogged o použití s LINQ na SQL zde:[http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/](http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/)

Chcete-li implementovat tuto techniku, otevřeme "Průzkumník serveru" v rámci sady Visual Studio, vyberte databázi NerdDinner a potom klikněte pravým tlačítkem myši na poduzel "funkce" pod ním a zvolte vytvořit novou funkci "Skalární hodnota":

![](use-ajax-to-implement-mapping-scenarios/_static/image8.png)

Vložíme do následující funkce DistanceBetween:

[!code-sql[Main](use-ajax-to-implement-mapping-scenarios/samples/sample7.sql)]

Vytvoříme novou funkci s hodnotou tabulky na serveru SQL Server, kterou budeme nazývat "NearestDinners":

![](use-ajax-to-implement-mapping-scenarios/_static/image9.png)

Tato funkce tabulky "NearestDinners" používá funkci DistanceBetween helper k vrácení všech večeří v okruhu 100 mil od zeměpisné šířky a délky, kterou dodáváme:

[!code-sql[Main](use-ajax-to-implement-mapping-scenarios/samples/sample8.sql)]

Chcete-li tuto funkci volat, nejprve otevřeme návrháře LINQ na SQL poklepáním na soubor NerdDinner.dbml v našem adresáři \Models:

![](use-ajax-to-implement-mapping-scenarios/_static/image10.png)

Budeme pak přetáhnout NearestDinners a DistanceBetween funkce na LINQ do SQL návrháře, což způsobí, že budou přidány jako metody na naší LINQ na SQL NerdDinnerDataContext třídy:

![](use-ajax-to-implement-mapping-scenarios/_static/image11.png)

Můžeme pak vystavit metodu dotazu "FindByLocation" na naší DinnerRepository třídy, která používá Funkce NearestDinner vrátit nadcházející Dinners, které jsou v rámci 100 mil od zadaného umístění:

[!code-csharp[Main](use-ajax-to-implement-mapping-scenarios/samples/sample9.cs)]

### <a name="implementing-a-json-based-ajax-search-action-method"></a>Implementace metody vyhledávání AJAX založené na JSON

Nyní implementujeme metodu akce kontroleru, která využívá novou metodu úložiště FindByLocation() k vrácení seznamu dat dinner, které lze použít k naplnění mapy. Budeme mít tuto metodu akce vrátit zpět data večeři ve formátu JSON (JavaScript Object Notation) tak, aby bylo možné snadno manipulovat pomocí JavaScriptu na straně klienta.

Chcete-li tento problém implementovat, vytvoříme novou třídu "SearchController" kliknutím pravým tlačítkem myši na adresář \Controllers a výběrem příkazu nabídky&gt;Přidat řadič. Poté implementujeme metodu akce "SearchByLocation" v rámci nové třídy SearchController, jako je následující:

[!code-csharp[Main](use-ajax-to-implement-mapping-scenarios/samples/sample10.cs)]

Metoda akce SearchController SearchByLocation interně volá metodu FindByLocation v DinnerRepository, aby získala seznam blízkých večeří. Spíše než vrátit Dinner objekty přímo klientovi, ale místo toho vrátí JsonDinner objekty. Třída JsonDinner zpřístupňuje podmnožinu vlastností Dinner (například: z bezpečnostních důvodů nezveřejňuje jména lidí, kteří mají RSVP'd pro večeři). Obsahuje také RSVPCount vlastnost, která neexistuje na Večeři – a který se dynamicky vypočítá počítáním počet RSVP objekty spojené s konkrétní večeři.

Potom používáme pomocnou metodu Json() v základní třídě řadiče k vrácení sekvence večeří pomocí formátu drátu založeného na JSON. JSON je standardní textový formát pro reprezentaci jednoduchých datových struktur. Níže je uveden příklad toho, co json formátovaný seznam dvou objektů JsonDinner vypadá při návratu z naší metody akce:

[!code-json[Main](use-ajax-to-implement-mapping-scenarios/samples/sample11.json)]

### <a name="calling-the-json-based-ajax-method-using-jquery"></a>Volání metody AJAX založené na JSON pomocí jQuery

Nyní jsme připraveni aktualizovat domovskou stránku aplikace NerdDinner, abychom použili metodu akce SearchController SearchByLocation. Chcete-li to provést, otevřeme šablonu zobrazení /Views/Home/Index.aspx a aktualizujeme ji tak, aby &lt;&gt; měla textové pole, tlačítko hledání, naši mapu a prvek div s názvem dinnerList:

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample12.aspx)]

Na stránku pak můžeme přidat dvě funkce JavaScriptu:

[!code-html[Main](use-ajax-to-implement-mapping-scenarios/samples/sample13.html)]

První funkce JavaScriptu načte mapu při prvním načtení stránky. Druhá funkce JavaScriptu napojit na obslužnou rutinu události kliknutí JavaScriptu na vyhledávacím tlačítku. Po stisknutí tlačítka volá FindDinnersGivenLocation() JavaScript funkce, kterou přidáme do našeho souboru Map.js:

[!code-javascript[Main](use-ajax-to-implement-mapping-scenarios/samples/sample14.js)]

Tato funkce FindDinnersGivenLocation() volá mapu. Find() na Virtuální Země control pro střed na zadaném místě. Když se vrátí služba virtuální mapy Země, mapa. Find() metoda vyvolá callbackUpdateMapDinners metodu zpětného volání jsme ji předaljako konečný argument.

CallbackUpdateMapDinners() Metoda je, kde se provádí skutečná práce. Používá jQuery $.post() pomocná metoda k provedení volání AJAX na naše SearchController SearchByLocation() akční metoda - předávání je zeměpisná šířka a délka nově vystředěné mapy. Definuje včleněnou funkci, která bude volána po dokončení pomocné metody $.post() a výsledky večeře ve formátu JSON vrácené z metody akce SearchByLocation() budou předány pomocí proměnné s názvem "dinners". Potom dělá foreach přes každou vrácenou večeři a používá šířku a délku večeře a další vlastnosti k přidání nového špendlíku na mapě. Přidá také večeři položku html seznamu večeří na pravé straně mapy. Potom napojit událost vznášení pro připínáčků i seznam HTML tak, aby se při nasazení uživatele zobrazovaly podrobnosti o večeři, když na ně uživatel najedou:

[!code-html[Main](use-ajax-to-implement-mapping-scenarios/samples/sample15.html)]

A teď, když spustíme aplikaci a navštívíme domovskou stránku, zobrazí se nám mapa. Když zadáme název města, mapa zobrazí nadcházející večeře v jeho blízkosti:

![](use-ajax-to-implement-mapping-scenarios/_static/image12.png)

Když najdete nad večeří, zobrazí se o ní podrobnosti.

Kliknutím na název večeře buď v bublině, nebo na pravé straně v seznamu HTML nás naviguje na večeři - což pak můžeme volitelně RSVP pro:

![](use-ajax-to-implement-mapping-scenarios/_static/image13.png)

### <a name="next-step"></a>Další krok

Nyní jsme implementovali všechny funkce aplikace aplikace NerdDinner. Podívejme se nyní na to, jak můžeme povolit automatizované testování částí.

> [!div class="step-by-step"]
> [Předchozí](use-ajax-to-deliver-dynamic-updates.md)
> [další](enable-automated-unit-testing.md)
