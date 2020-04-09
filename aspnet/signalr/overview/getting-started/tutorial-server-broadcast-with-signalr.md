---
uid: signalr/overview/getting-started/tutorial-server-broadcast-with-signalr
title: 'Výuka: Vysílání serveru s SignalR 2 | Dokumenty společnosti Microsoft'
author: tdykstra
description: Tento kurz ukazuje, jak vytvořit webovou aplikaci, která používá ASP.NET SignalR 2 poskytovat funkce vysílání serveru.
ms.author: bradyg
ms.date: 01/02/2019
ms.topic: tutorial
ms.assetid: 1568247f-60b5-4eca-96e0-e661fbb2b273
msc.legacyurl: /signalr/overview/getting-started/tutorial-server-broadcast-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: 14924109fff8db3e537e6bc08b6dc868792ee660
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676095"
---
# <a name="tutorial-server-broadcast-with-signalr-2"></a>Výuka: Vysílání serveru se signálem2

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

Tento kurz ukazuje, jak vytvořit webovou aplikaci, která používá ASP.NET SignalR 2 poskytovat funkce vysílání serveru. Vysílání serveru znamená, že server spustí komunikaci odeslanou klientům.

Aplikace, kterou vytvoříte v tomto kurzu simuluje burzovní burzovní burzovní, typický scénář pro funkce vysílání serveru. Server pravidelně náhodně aktualizuje ceny akcií a vysílá aktualizace všem připojeným klientům. V prohlížeči se čísla a symboly v **change** a **%** sloupcích dynamicky mění v reakci na oznámení ze serveru. Pokud otevřete další prohlížeče na stejnou adresu URL, zobrazí se všechna stejná data a stejné změny dat současně.

![Vytvořit web](tutorial-server-broadcast-with-signalr/_static/image1.png)

V tomto kurzu jste:

> [!div class="checklist"]
> * Vytvoření projektu
> * Nastavení kódu serveru
> * Zkontrolujte kód serveru
> * Nastavení kódu klienta
> * Zkontrolujte kód klienta
> * Testování aplikace
> * Povolit protokolování

> [!IMPORTANT]
> Pokud nechcete pracovat přes kroky vytváření aplikace, můžete nainstalovat SignalR.Sample balíček v novém projektu Prázdné ASP.NET webová aplikace. Pokud nainstalujete balíček NuGet bez provedení kroků v tomto kurzu, je nutné postupovat podle pokynů v souboru *readme.txt.* Chcete-li spustit balíček, musíte přidat spouštěcí `ConfigureSignalR` třídu OWIN, která volá metodu v nainstalovaném balíčku. Pokud nepřidáte spouštěcí třídu OWIN, zobrazí se chyba. Viz [instalace ukázkové části StockTicker](#install-the-stockticker-sample) v tomto článku.

## <a name="prerequisites"></a>Požadavky

* Sada [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) se sadou funkcí **Vývoj pro ASP.NET a web**.

## <a name="create-the-project"></a>Vytvoření projektu

Tato část ukazuje, jak pomocí sady Visual Studio 2017 vytvořit prázdnou ASP.NET webovou aplikaci.

1. V sadě Visual Studio vytvořte ASP.NET webovou aplikaci.

    ![Vytvořit web](tutorial-server-broadcast-with-signalr/_static/image2.png)

1. V okně **Nová ASP.NET webová aplikace - SignalR.StockTicker** ponechejte **prázdné** vybrané a vyberte **OK**.

## <a name="set-up-the-server-code"></a>Nastavení kódu serveru

V této části nastavíte kód, který běží na serveru.

### <a name="create-the-stock-class"></a>Vytvoření třídy Stock

Začnete vytvořením třídy *stock* modelu, kterou použijete k ukládání a přenosu informací o akciích.

1. V **Průzkumníku řešení**klepněte pravým tlačítkem myši na projekt a vyberte **přidat** > **třídu**.

1. Pojmenujte třídu *Stock* a přidejte ji do projektu.

1. Nahraďte kód v *souboru Stock.cs* tímto kódem:

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample1.cs)]

    Dvě vlastnosti, které nastavíte při `Symbol` vytváření akcií, jsou (například `Price`MSFT pro Microsoft) a . Ostatní vlastnosti závisí na tom, jak a kdy nastavíte `Price`. Při prvním nastavení `Price`se hodnota rozšíří na `DayOpen`. `Price`Poté, když nastavíte , aplikace `Change` `PercentChange` vypočítá hodnoty vlastností `Price` a `DayOpen`na základě rozdílu mezi a .

### <a name="create-the-stocktickerhub-and-stockticker-classes"></a>Vytvoření tříd StockTickerHub a StockTicker

K zpracování interakce mezi serverem a klientem budete používat rozhraní API hubu SignalR. Třída, `StockTickerHub` která je odvozena `Hub` od třídy SignalR bude zpracovávat přijímající připojení a volání metod z klientů. Je také nutné udržovat data `Timer` zásob a spustit objekt. Objekt `Timer` bude pravidelně spouštět aktualizace cen nezávisle na připojení klientů. Tyto funkce nelze umístit do `Hub` třídy, protože centra jsou přechodné. Aplikace vytvoří `Hub` instanci třídy pro každou úlohu v rozbočovači, jako jsou připojení a volání z klienta na server. Takže mechanismus, který uchovává data o akciích, aktualizuje ceny a vysílá aktualizace cen, musí být spuštěn v samostatné třídě. Pojmenujete třídu `StockTicker`.

![Vysílání z StockTicker](tutorial-server-broadcast-with-signalr/_static/image3.png)

Chcete spustit pouze jednu instanci `StockTicker` třídy na serveru, takže budete muset `StockTickerHub` nastavit odkaz z `StockTicker` každé instance na instanci singleton. Třída `StockTicker` musí vysílat klientům, protože má skladová data `StockTicker` a aktivuje `Hub` aktualizace, ale není třída. Třída `StockTicker` musí získat odkaz na objekt kontextu připojení signalr hub. Potom můžete použít objekt kontextu připojení SignalR k vysílání klientům.

#### <a name="create-stocktickerhubcs"></a>Vytvořit StockTickerHub.cs

1. V **Průzkumníku řešení**klepněte pravým tlačítkem myši na projekt a vyberte **přidat** > **novou položku**.

1. V **přidejte novou položku - SignalR.StockTicker**vyberte **nainstalovaný** > **vizuální C#** > **Web** > **SignalR** a pak vyberte **Třída rozbočovače SignalR (v2)**.

1. Pojmenujte třídu *StockTickerHub* a přidejte ji do projektu.

    Tento krok vytvoří soubor *třídy StockTickerHub.cs.* Současně přidá sadu souborů skriptů a odkazy na sestavení, které podporují SignalR do projektu.

1. Nahraďte kód v *souboru StockTickerHub.cs* tímto kódem:

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample2.cs)]

1. Uložte soubor.

Aplikace používá třídu [Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx) k definování metod, které mohou klienti volat na serveru. Definujete jednu metodu: `GetAllStocks()`. Když se klient zpočátku připojí k serveru, zavolá tuto metodu, aby získal seznam všech akcií s aktuálními cenami. Metoda může být spuštěna synchronně a vrátit, `IEnumerable<Stock>` protože vrací data z paměti.

Pokud metoda měla získat data tím, že dělá něco, co by znamenalo čekání, jako `Task<IEnumerable<Stock>>` je vyhledávání databáze nebo volání webové služby, byste zadat jako vrácenou hodnotu povolit asynchronní zpracování. Další informace naleznete [v tématu ASP.NET SignalR Hubs API Guide - Server - Při spuštění asynchronně](../guide-to-the-api/hubs-api-guide-server.md#asyncmethods).

Atribut `HubName` určuje, jak bude aplikace odkazovat na hub v kódu JavaScriptu na straně klienta. Výchozí název na straně klienta, pokud tento atribut nepoužíváte, je camelCase verze názvu `stockTickerHub`třídy, která by v tomto případě byla .

Jak uvidíte později při `StockTicker` vytváření třídy, aplikace vytvoří singleton instanci této třídy v jeho statické `Instance` vlastnosti. Tato instance singleton `StockTicker` je v paměti bez ohledu na to, kolik klientů se připojí nebo odpojí. Tato instance je `GetAllStocks()` to, co metoda používá k vrácení aktuální informace o zásobách.

#### <a name="create-stocktickercs"></a>Vytvořit StockTicker.cs

1. V **Průzkumníku řešení**klepněte pravým tlačítkem myši na projekt a vyberte **přidat** > **třídu**.

1. Pojmenujte třídu *StockTicker* a přidejte ji do projektu.

1. Nahraďte kód v *souboru StockTicker.cs* tímto kódem:

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample3.cs)]

Vzhledem k tomu, že všechna vlákna budou spuštěna ve stejné instanci kódu StockTicker, musí být třída StockTicker bezpečná pro přístup z více vláken.

### <a name="examine-the-server-code"></a>Zkontrolujte kód serveru

Pokud zkontrolujete kód serveru, pomůže vám to pochopit, jak aplikace funguje.

#### <a name="storing-the-singleton-instance-in-a-static-field"></a>Uložení instance singletonu do statického pole

Kód inicializuje statické `_instance` pole, které `Instance` podporuje vlastnost s instancí třídy. Protože konstruktor je soukromý, je to jediná instance třídy, kterou může aplikace vytvořit. Aplikace používá [opožděné inicializace](/dotnet/framework/performance/lazy-initialization) pro `_instance` pole. Není to z důvodů výkonu. Je to ujistěte se, že vytvoření instance je bezpečné pro přístup z více vláken.

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample4.cs)]

Pokaždé, když se klient připojí k serveru, nová instance třídy StockTickerHub spuštěné v samostatném `StockTicker.Instance` vlákně získá instanci `StockTickerHub` singleton StockTicker ze statické vlastnosti, jak jste viděli dříve ve třídě.

#### <a name="storing-stock-data-in-a-concurrentdictionary"></a>Ukládání skladových dat v concurrentdictionary

Konstruktor inicializuje `_stocks` kolekci s některými `GetAllStocks` ukázkovými skladovými daty a vrátí zásoby. Jak jste viděli dříve, tato kolekce `StockTickerHub.GetAllStocks`zásob je vrácena `Hub` , což je serverová metoda ve třídě, kterou mohou klienti volat.

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample5.cs)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample6.cs)]

Kolekce zásob je definována jako [concurrentdictionary](https://msdn.microsoft.com/library/dd287191.aspx) typ pro bezpečnost podprocesu. Jako alternativu můžete použít [Dictionary](https://msdn.microsoft.com/library/xfhwa508.aspx) objekt a explicitně zamknout slovník při provádění změn v něm.

Pro tuto ukázkovou aplikaci je v pořádku ukládat data aplikace do paměti `StockTicker` a ztratit data, když aplikace nakládá s instancí. V reálné aplikaci byste pracovat s úložiště dat back-end jako databáze.

#### <a name="periodically-updating-stock-prices"></a>Pravidelná aktualizace cen akcií

Konstruktor spustí `Timer` objekt, který pravidelně volá metody, které aktualizují ceny akcií nanáhodném základě.

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample7.cs)]

 `Timer`volání `UpdateStockPrices`, která předává hodnotu null v parametru stavu. Před aktualizací cen aplikace zamyká `_updateStockPricesLock` objekt. Kód zkontroluje, zda jiné vlákno již aktualizuje `TryUpdateStockPrice` ceny a pak volá na každé zásoby v seznamu. Metoda `TryUpdateStockPrice` rozhodne, zda změnit cenu akcií, a kolik ji změnit. Pokud se cena akcií změní, aplikace zavolá `BroadcastStockPrice` k vysílání změny ceny akcií všem připojeným klientům.

Příznak `_updatingStockPrices` označený [volatile,](https://msdn.microsoft.com/library/x13ttww7.aspx) aby se ujistil, že je bezpečný pro přístup z více vláken.

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample8.cs)]

V reálné aplikaci `TryUpdateStockPrice` by metoda volala webovou službu, aby vyhledává cenu. V tomto kódu aplikace používá generátor náhodných čísel k náhodným změnám.

#### <a name="getting-the-signalr-context-so-that-the-stockticker-class-can-broadcast-to-clients"></a>Získání kontextu SignalR tak, aby třída StockTicker může vysílat klientům

Vzhledem k tomu, že `StockTicker` změny cen pocházejí zde v objektu, je to objekt, který potřebuje volat metodu `updateStockPrice` na všechny připojené klienty. Ve `Hub` třídě máte rozhraní API pro volání `StockTicker` klientských metod, `Hub` ale není odvozeno z třídy a nemá odkaz na žádný `Hub` objekt. Chcete-li vysílat do `StockTicker` připojených klientů, třída musí `StockTickerHub` získat instance kontextu SignalR pro třídu a použít ji k volání metod na klienty.

Kód získá odkaz na kontext SignalR při vytvoření instance třídy singleton, předá tento odkaz na `Clients` konstruktoru a konstruktor jej vloží do vlastnosti.

Existují dva důvody, proč chcete získat kontext pouze jednou: získání kontextu je nákladný úkol a získání jednou zajistí, že aplikace zachová zamýšlené pořadí zpráv odeslaných klientům.

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample9.cs)]

Získání `Clients` vlastnost kontextu a jeho vložení `StockTickerClient` do vlastnosti umožňuje psát kód pro volání klientských `Hub` metod, které vypadají stejně jako ve třídě. Chcete-li například vysílat všem `Clients.All.updateStockPrice(stock)`klientům, můžete psát .

Metoda, `updateStockPrice` kterou voláte, `BroadcastStockPrice` ještě neexistuje. Přidáte jej později při psaní kódu, který běží na straně klienta. Můžete odkazovat `updateStockPrice` zde, protože `Clients.All` je dynamický, což znamená, že aplikace vyhodnotí výraz za běhu. Při spuštění tohoto volání metody SignalR odešle název metody a hodnotu parametru klientovi `updateStockPrice`a pokud má klient metodu s názvem , aplikace zavolá tuto metodu a předá jí hodnotu parametru.

`Clients.All`znamená poslat všem klientům. SignalR poskytuje další možnosti určit, které klienty nebo skupiny klientů chcete odeslat. Další informace naleznete v tématu [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx).

### <a name="register-the-signalr-route"></a>Registrace trasy SignalR

Server potřebuje vědět, která adresa URL zachytit a přímo signalr. Chcete-li to provést, přidejte spouštěcí třídu OWIN:

1. V **Průzkumníku řešení**klepněte pravým tlačítkem myši na projekt a vyberte **přidat** > **novou položku**.

1. V **pole Přidat novou položku - SignalR.StockTicker** vyberte **nainstalovaný** > **visual c#** > **web** a pak vyberte **OWIN Startup Class**.

1. Pojmenujte položku *Spuštění* a vyberte **ok**.

1. Nahraďte výchozí kód v *souboru Startup.cs* tímto kódem:

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample10.cs)]

Nyní jste dokončili nastavení kódu serveru. V další části nastavíte klienta.

## <a name="set-up-the-client-code"></a>Nastavení kódu klienta

V této části nastavíte kód, který běží na straně klienta.

### <a name="create-the-html-page-and-javascript-file"></a>Vytvoření stránky HTML a souboru JavaScriptu

Stránka HTML zobrazí data a soubor JavaScript uvede data.

#### <a name="create-stocktickerhtml"></a>Vytvořit stockticker.html

Nejprve přidáte klienta HTML.

1. V **Průzkumníku řešení**klepněte pravým tlačítkem myši na projekt a vyberte **přidat** > **stránku HTML**.

1. Pojmenujte soubor *StockTicker* a vyberte **OK**.

1. Nahraďte výchozí kód v souboru *StockTicker.html* tímto kódem:

    [!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample11.html?highlight=40-43)]

    Html vytvoří tabulku s pěti sloupci, řádek záhlaví a datový řádek s jednou buňkou, která pokrývá všech pět sloupců. Na řádku dat se zobrazuje "načítání..." chvíli při spuštění aplikace. Kód JavaScriptu tento řádek odstraní a přidá na jeho místo řádky s daty zásob načtenými ze serveru.

    Značky skriptů určují:

    * Soubor skriptu jQuery.

    * Základní skript SignalR.

    * Soubor skriptu proxy SignalR.

    * Soubor skriptu StockTicker, který vytvoříte později.

    Aplikace dynamicky generuje soubor skriptu proxy signalr. Určuje adresu URL "/signalr/hubs" a definuje metody proxy pro metody na hub `StockTickerHub.GetAllStocks`třídy, v tomto případě pro . Pokud chcete, můžete tento soubor JavaScript vygenerovat ručně pomocí [signalr utilities](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/). Nezapomeňte zakázat dynamické vytváření souborů `MapHubs` ve volání metody.

1. V **Průzkumníku řešení**rozbalte **položku Skripty**.

    Skriptknihovny pro jQuery a SignalR jsou viditelné v projektu.

    > [!IMPORTANT]
    > Správce balíčků nainstaluje novější verzi skriptů SignalR.

1. Aktualizujte odkazy na skripty v bloku kódu tak, aby odpovídaly verzím souborů skriptů v projektu.

1. V **Průzkumníku řešení**klepněte pravým tlačítkem myši na *soubor StockTicker.html*a pak vyberte **příkaz Nastavit jako úvodní stránku**.

#### <a name="create-stocktickerjs"></a>Vytvořit soubor StockTicker.js

Nyní vytvořte soubor JavaScriptu.

1. V **Průzkumníku řešení**klepněte pravým tlačítkem myši na projekt a vyberte **přidat** > **soubor JavaScript .**

1. Pojmenujte soubor *StockTicker* a vyberte **OK**.

1. Přidejte tento kód do souboru *StockTicker.js:*

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample12.js)]

### <a name="examine-the-client-code"></a>Zkontrolujte kód klienta

Pokud zkontrolujete kód klienta, pomůže vám zjistit, jak klientský kód spolupracuje s kódem serveru, aby aplikace fungovala.

#### <a name="starting-the-connection"></a>Spuštění připojení

`$.connection`odkazuje na proxy servery SignalR. Kód získá odkaz na proxy `StockTickerHub` pro třídu a `ticker` vloží jej do proměnné. Název proxy serveru je název, `HubName` který byl nastaven atributem:

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample13.js)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample14.cs)]

Po definování všech proměnných a funkcí poslední řádek kódu v souboru inicializuje připojení `start` SignalR voláním funkce SignalR. Funkce `start` se spustí asynchronně a vrátí [jQuery Odložené objektu](http://api.jquery.com/category/deferred-object/). Můžete volat hotovou funkci a určit funkci, která má být volána, když aplikace dokončí asynchronní akci.

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample15.js)]

#### <a name="getting-all-the-stocks"></a>Získání všech zásob

Funkce `init` volá `getAllStocks` funkci na serveru a používá informace, které server vrátí k aktualizaci burzovní tabulky. Všimněte si, že ve výchozím nastavení je třeba použít camelCasing na straně klienta, i když název metody je pascal-cased na serveru. Pravidlo camelCasing se vztahuje pouze na metody, nikoli na objekty. Například odkazujete `stock.Symbol` na `stock.Price`a `stock.symbol` `stock.price`, not nebo .

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample16.js)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample17.cs)]

V `init` metodě aplikace vytvoří HTML pro řádek tabulky pro každý skladový objekt přijatý `formatStock` ze serveru voláním do formátu `rowTemplate` vlastností `stock` `stock` objektu a pak voláním `supplant` nahradit zástupné symboly v proměnné hodnotami vlastností objektu. Výsledný kód HTML je pak připojen k burzovní tabulce.

> [!NOTE]
> Volání `init` předáním jako `callback` funkce, která se spustí po `start` dokončení asynchronní funkce. Pokud jste `init` po volání `start`volali jako samostatný příkaz JavaScript , funkce by se nezdaří, protože by se spustila okamžitě, aniž by čekala na dokončení počáteční funkce připojení. V takovém případě `init` by se funkce `getAllStocks` pokusila volat funkci předtím, než aplikace naváže připojení k serveru.

#### <a name="getting-updated-stock-prices"></a>Získání aktualizovaných cen akcií

Když server změní cenu akcie, zavolá `updateStockPrice` na připojené klienty. Aplikace přidá funkci do vlastnosti `stockTicker` klienta proxy serveru, aby byla k dispozici pro volání ze serveru.

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample18.js)]

Funkce `updateStockPrice` formátuje skladový objekt přijatý ze serveru do řádku tabulky `init` stejným způsobem jako ve funkci. Místo připojení řádku k tabulce najde aktuální řádek akcie v tabulce a nahradí tento řádek novým.

## <a name="test-the-application"></a>Testování aplikace

Aplikaci můžete otestovat, abyste se ujistili, že funguje. Zobrazí se ve všech oknech prohlížeče, kde se zobrazí tabulka živých akcií s kolísavými cenami akcií.

1. Na panelu nástrojů zapněte ladění **skriptů** a pak vyberte tlačítko přehrát pro spuštění aplikace v režimu ladění.

    ![Snímek obrazovky s uživatelem, který zapne režim ladění a vybere možnost Přehrát.](tutorial-server-broadcast-with-signalr/_static/image4.png)

    Otevře se okno prohlížeče s živou **skladovou tabulkou**. Tabulka zásob zpočátku zobrazuje "loading..." line, pak, po krátké době, aplikace zobrazí počáteční údaje o akciích, a pak ceny akcií začnou měnit.

1. Zkopírujte adresu URL z prohlížeče, otevřete dva další prohlížeče a vložte adresy URL do panelů adresaí.

    Počáteční zobrazení zásob je stejné jako první prohlížeč a změny se dějí současně.

1. Zavřete všechny prohlížeče, otevřete nový prohlížeč a přejděte na stejnou adresu URL.

    StockTicker singleton objekt pokračoval v běhu na serveru. **Tabulka živých akcií** ukazuje, že zásoby se nadále mění. Nevidíte počáteční tabulku s nulovými změnami.

1. Zavřete prohlížeč.

## <a name="enable-logging"></a>Povolit protokolování

SignalR má vestavěnou funkci protokolování, kterou můžete povolit na straně klienta na pomoc při řešení potíží. V této části povolíte protokolování a zobrazí tepříklady, které ukazují, jak protokoly zjistit, které z následujících metod přenosu SignalR používá:

* [WebSockets](http://en.wikipedia.org/wiki/WebSocket), podporované službou IIS 8 a aktuálními prohlížeči.

* [Události odeslané serverem](http://en.wikipedia.org/wiki/Server-sent_events)podporované jinými prohlížeči než internet explorer.

* [Forever frame](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe), podporovaný aplikací Internet Explorer.

* [Ajax dlouhé dotazování](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling), podporované všemi prohlížeči.

Pro dané připojení SignalR zvolí nejlepší způsob přenosu, který server i klient podporují.

1. Otevřete *soubor StockTicker.js*.

1. Přidejte tento zvýrazněný řádek kódu, který povolí protokolování bezprostředně před kódem, který inicializuje připojení na konci souboru:

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample19.js?highlight=2)]

1. Spuštění projektu stisknutím **klávesy F5.**

1. Otevřete okno vývojářských nástrojů prohlížeče a vyberte konzolu, chcete-li protokoly zobrazit. Bude pravděpodobně nutné aktualizovat stránku zobrazíte protokoly SignalR vyjednávání způsob přenosu pro nové připojení.

    * Pokud používáte aplikaci Internet Explorer 10 v systému Windows 8 (IIS 8), je způsob přenosu **WebSockets**.

    * Pokud používáte aplikaci Internet Explorer 10 v systému Windows 7 (IIS 7.5), je způsob přenosu **iframe**.

    * Pokud používáte Firefox 19 ve Windows 8 (IIS 8), je způsob přenosu **WebSockets**.

        > [!TIP]
        > Ve Firefoxu nainstalujte doplněk Firebug, abyste získali okno konzoly.

    * Pokud používáte Firefox 19 v systému Windows 7 (IIS 7.5), způsob přenosu je **událost mizející serverem.**

## <a name="install-the-stockticker-sample"></a>Instalace ukázky StockTicker

[Microsoft.AspNet.SignalR.Sample](http://nuget.org/packages/microsoft.aspnet.signalr.sample) nainstaluje aplikaci StockTicker. Balíček NuGet obsahuje více funkcí než zjednodušená verze, kterou jste vytvořili od začátku. V této části kurzu nainstalujete balíček NuGet a zkontrolujte nové funkce a kód, který je implementuje.

> [!IMPORTANT]
> Pokud nainstalujete balíček bez provedení předchozíkroky tohoto kurzu, je nutné přidat spouštěcí třídy OWIN do projektu. Tento soubor readme.txt pro balíček NuGet vysvětluje tento krok.

### <a name="install-the-signalrsample-nuget-package"></a>Instalace balíčku SignalR.Sample NuGet

1. V **Průzkumníku řešení**klepněte pravým tlačítkem myši na projekt a vyberte **příkaz Spravovat balíčky NuGet**.

1. Ve **správci balíčků NuGet: SignalR.StockTicker**vyberte **Procházet**.

1. Ve **zdroji balíčku**vyberte **nuget.org**.

1. Do vyhledávacího pole zadejte *položku SignalR.Sample* a vyberte **položku Microsoft.AspNet.SignalR.Sample** > **Install**.

1. V **Průzkumníku řešení**rozbalte složku *SignalR.Sample.*

    Instalace balíčku SignalR.Sample vytvořila složku a její obsah.

1. Ve složce *SignalR.Sample* klepněte pravým tlačítkem myši na *soubor StockTicker.html*a pak vyberte **příkaz Nastavit jako úvodní stránku**.

    > [!NOTE]
    > Instalace balíčku SignalR.Sample NuGet může změnit verzi jQuery, kterou máte ve složce *Skripty.* Nový soubor *StockTicker.html,* který balíček nainstaluje do složky *SignalR.Sample,* bude synchronizován s verzí jQuery, kterou balíček nainstaluje, ale pokud chcete znovu spustit původní soubor *StockTicker.html,* budete muset nejprve aktualizovat odkaz jQuery ve značce skriptu.

### <a name="run-the-application"></a>Spuštění aplikace

 Tabulka, kterou jste viděli v první aplikaci, měla užitečné funkce. Plná burzovní aplikace zobrazuje nové funkce: vodorovně rolovací okno, které zobrazuje údaje o zásobách a zásoby, které mění barvu, když stoupají a klesají.

1. Stisknutím **klávesy F5** aplikaci spusťte.

     Při prvním spuštění aplikace je "trh" "zavřený" a zobrazí se statická tabulka a okno, které se neposouvá.

1. Vyberte **možnost Otevřít trh**.

    ![Snímek obrazovky s živým telegrafem](tutorial-server-broadcast-with-signalr/_static/image5.png)

    * Pole **Live Stock Ticker** se začne posouvat vodorovně a server začne náhodně vysílat změny cen akcií.

    * Pokaždé, když se změní cena akcií, aplikace aktualizuje **tabulku živých akcií** i **službu Live Stock Ticker**.

    * Když je změna ceny akcie kladná, aplikace zobrazí akcie se zeleným pozadím.

    * Když je změna záporná, aplikace zobrazí akcie s červeným pozadím.

1. Vyberte **Zavřít trh**.

    * Aktualizace tabulky se zastaví.

    * Ticker přestane posouvání.

1. Vyberte **Resetovat**.

    * Všechna skladová data jsou resetována.

    * Aplikace obnoví počáteční stav před zahájením změn cen.

1. Zkopírujte adresu URL z prohlížeče, otevřete dva další prohlížeče a vložte adresy URL do panelů adresaí.

1. V každém prohlížeči se dynamicky aktualizují stejná data současně.

1. Když vyberete některý z ovládacích prvků, všechny prohlížeče reagují stejným způsobem současně.

### <a name="live-stock-ticker-display"></a>Živý burzovní displej

Zobrazení **Live Stock Ticker** je neuspořádaný seznam v `<div>` prvku formátovaném do jednoho řádku styly CSS. Aplikace inicializuje a aktualizuje ticker stejným způsobem jako tabulka: nahrazením `<li>` zástupných symbolů `<li>` v řetězci šablony a dynamickým přidáním prvků do `<ul>` prvku. Aplikace zahrnuje posouvání pomocí funkce `animate` jQuery, která mění okraj vlevo od `<div>`neuspořádaného seznamu v rámci .

#### <a name="signalrsample-stocktickerhtml"></a>SignalR.Sample StockTicker.html

Html kód burzovního poletoru:

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample20.html)]

#### <a name="signalrsample-stocktickercss"></a>SignalR.Sample StockTicker.css

Burzovní kód CSS:

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample21.html)]

#### <a name="signalrsample-signalrstocktickerjs"></a>SignalR.Sample SignalR.StockTicker.js

JQuery kód, který dělá to posun:

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample22.js)]

### <a name="additional-methods-on-the-server-that-the-client-can-call"></a>Další metody na serveru, které může klient volat

Chcete-li aplikaci zvýšit flexibilitu, existují další metody, které může aplikace volat.

#### <a name="signalrsample-stocktickerhubcs"></a>SignalR.Sample StockTickerHub.cs

Třída `StockTickerHub` definuje čtyři další metody, které může klient volat:

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample23.cs)]

Aplikace volá `OpenMarket` `CloseMarket`, `Reset` a v reakci na tlačítka v horní části stránky. Ukazují vzor jednoho klienta, který aktivuje změnu stavu, která je okamžitě rozšířena na všechny klienty. Každá z těchto metod volá `StockTicker` metodu ve třídě, která způsobuje změnu stavu trhu a poté vysílá nový stav.

#### <a name="signalrsample-stocktickercs"></a>SignalR.Sample StockTicker.cs

Ve `StockTicker` třídě aplikace udržuje stav trhu s vlastností, `MarketState` která `MarketState` vrací hodnotu výčtu:

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample24.cs)]

Každá z metod, které mění stav trhu, tak `StockTicker` činí uvnitř bloku zámku, protože třída musí být bezpečná pro přístup z více vláken:

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample25.cs)]

Chcete-li se ujistit, že `_marketState` tento kód `MarketState` je `volatile`bezpečný pro přístup z více vláken, pole, které podporuje vlastnost určenou :

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample26.cs)]

Metody `BroadcastMarketStateChange` `BroadcastMarketReset` a jsou podobné metodě BroadcastStockPrice, kterou jste již viděli, s výjimkou volání různých metod definovaných na straně klienta:

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample27.cs)]

### <a name="additional-functions-on-the-client-that-the-server-can-call"></a>Další funkce v klientovi, které může server volat

Funkce `updateStockPrice` nyní zpracovává tabulku i ticker displej a `jQuery.Color` používá k blikání červené a zelené barvy.

Nové funkce v *Souboru SignalR.StockTicker.js* povolit a zakázat tlačítka na základě stavu trhu. Oni také zastavit nebo spustit **Live Stock Ticker** horizontální rolování. Vzhledem k tomu, `ticker.client`že mnoho funkcí jsou přidávány do aplikace používá [jQuery rozšířit funkci](http://api.jquery.com/jQuery.extend/) přidat.

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample28.js)]

### <a name="additional-client-setup-after-establishing-the-connection"></a>Další nastavení klienta po navázání připojení

Poté, co klient naváže připojení, má některé další práce provést:

* Zjistěte, zda je trh otevřený nebo `marketOpened` `marketClosed` uzavřený, abyste zavolali příslušnou nebo funkci.

* Připojte volání metody serveru k tlačítkům.

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample29.js)]

Metody serveru nejsou připojeny k tlačítkům až poté, co aplikace naváže připojení. Je to tak, že kód nemůže volat metody serveru dříve, než jsou k dispozici.

## <a name="additional-resources"></a>Další zdroje

V tomto kurzu jste se naučili, jak naprogramovat aplikaci SignalR, která vysílá zprávy ze serveru všem připojeným klientům. Nyní můžete vysílat zprávy v pravidelných intervalech a v reakci na oznámení od libovolného klienta. Koncept vícevláknové instance singleton uchovávat stav serveru ve scénářích online her pro více hráčů. Viz [například hra ShootR založená na SignalR](https://github.com/NTaylorMullen/ShootR).

Kurzy, které zobrazují scénáře komunikace mezi dvěma účastníky, naleznete [v tématu Začínáme s SignalR](introduction-to-signalr.md) a [Aktualizace v reálném čase s SignalR](tutorial-high-frequency-realtime-with-signalr.md).

Další informace o SignalR naleznete v následujících zdrojích:

* [ASP.NET SignalR](../../index.md)
* [Projekt SignalR](http://signalr.net/)
* [SignalR GitHub a ukázky](https://github.com/SignalR/SignalR)
* [SignalR Wiki](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a>Další kroky

V tomto kurzu jste:

> [!div class="checklist"]
> * Byl vytvořen projekt
> * Nastavení kódu serveru
> * Zkontrolovánkód serveru
> * Nastavení kódu klienta
> * Zkontrolován kód klienta
> * Otestování aplikace
> * Povolené protokolování

Přejdete k dalšímu článku a dozvíte se, jak vytvořit webovou aplikaci v reálném čase, která používá ASP.NET SignalR 2.
> [!div class="nextstepaction"]
> [Vytvoření webové aplikace v reálném čase s SignalR](real-time-web-applications-with-signalr.md)
