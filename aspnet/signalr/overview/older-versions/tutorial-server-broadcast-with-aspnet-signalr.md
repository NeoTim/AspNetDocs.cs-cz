---
uid: signalr/overview/older-versions/tutorial-server-broadcast-with-aspnet-signalr
title: 'Kurz: Serverové vysílání s knihovnou ASP.NET SignalR 1.x | Dokumentace Microsoftu'
author: bradygaster
description: Tento kurz ukazuje, jak vytvořit webovou aplikaci, která používá knihovnu ASP.NET SignalR pro zajištění všesměrového vysílání funkce serveru. Serverové vysílání znamená, že to communic...
ms.author: bradyg
ms.date: 04/10/2013
ms.assetid: ab7b2554-956a-4f6d-b2a0-4ae0c62e8580
msc.legacyurl: /signalr/overview/older-versions/tutorial-server-broadcast-with-aspnet-signalr
msc.type: authoredcontent
ms.openlocfilehash: 258a55bf72c4b3425d001f478620fa9651952b3f
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57076096"
---
<a name="tutorial-server-broadcast-with-aspnet-signalr-1x"></a>Kurz: Serverové vysílání s knihovnou ASP.NET SignalR 1.x
====================
podle [Patrick Fletcher](https://github.com/pfletcher), [Petr Dykstra](https://github.com/tdykstra)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Tento kurz ukazuje, jak vytvořit webovou aplikaci, která používá knihovnu ASP.NET SignalR pro zajištění všesměrového vysílání funkce serveru. Server vysílání znamená, že komunikace klientů jsou spuštěné na serveru. Tento scénář vyžaduje jiný přístup programovací než peer-to-peer scénářů, jako je chatovací aplikace, ve kterých lze inicializovat komunikace klientů pomocí jedné nebo více klientů.
> 
> Aplikace, kterou vytvoříte v tomto kurzu simuluje akciích Typický scénář pro vysílání funkce serveru.
> 
> Si mohou komentáře u tohoto kurzu. Pokud máte nějaké otázky, které přímo nesouvisejí, najdete v tomto kurzu, můžete je publikovat [fórum ASP.NET SignalR](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) nebo [StackOverflow.com](http://stackoverflow.com).


## <a name="overview"></a>Přehled

[Microsoft.AspNet.SignalR.Sample](http://nuget.org/packages/microsoft.aspnet.signalr.sample) nainstaluje balíček NuGet ukázkové simulované aplikace běžícími v projektu sady Visual Studio. V první části tohoto kurzu vytvoříte zjednodušenou verzi této aplikace od začátku. Ve zbývající části tohoto kurzu budete instalovat balíček NuGet a zkontrolujte další funkce a kód, který vytvoří.

Aplikace akciích reprezentovala druh aplikací v reálném čase, ve kterém chcete pravidelně "push" nebo všesměrové vysílání, oznámení ze serveru na všechny připojené klienty.

Aplikace, na kterém budete stavět v první části tohoto kurzu zobrazí mřížku s uložených dat.

![Počáteční verze StockTicker](tutorial-server-broadcast-with-aspnet-signalr/_static/image1.png)

Server pravidelně náhodně aktualizuje ceny akcií a nabízených oznámení aktualizace na všechny připojené klienty. V prohlížeči čísla a symboly **změnit** a **%** dynamicky měnit sloupce v reakci na oznámení ze serveru. Pokud otevřete další prohlížeče pro stejnou adresu URL, všechny zobrazit stejná data a stejné změny dat současně.

Tento kurz obsahuje následující části:

- [Požadavky](#prerequisites)
- [Vytvoření projektu](#createproject)
- [Přidání balíčků SignalR NuGet](#nugetpackages)
- [Nastavte si do kódu serveru](#server)
- [Nastavit kód klienta](#client)
- [Testování aplikace](#test)
- [Povolení protokolování](#enablelogging)
- [Instalace a zkontrolujte úplnou ukázku StockTicker](#fullsample)
- [Další postup](#nextsteps)

> [!NOTE]
> Pokud nechcete, aby pro seznámení se základními kroky při vytváření aplikace, můžete nainstalovat balíček SignalR.Sample v novém **prázdná webová aplikace ASP.NET** projektu a přečtěte si vysvětlení kódu těchto kroků. První část kurzu obsahuje podmnožinu SignalR.Sample kódu a druhá část vysvětluje klíčové funkce v balíčku SignalR.Sample další funkce.


<a id="prerequisites"></a>

## <a name="prerequisites"></a>Požadavky

Než začnete, ujistěte se, že máte sadu Visual Studio 2012 nebo 2010 SP1 nainstalovaný ve vašem počítači. Pokud nemáte Visual Studio, přečtěte si téma [ASP.NET stáhne](https://www.asp.net/downloads) získat na bezplatné sady Visual Studio 2012 Express pro Web.

Pokud máte Visual Studio 2010, ujistěte se, že [NuGet](https://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c) je nainstalována.

<a id="createproject"></a>

## <a name="create-the-project"></a>Vytvoření projektu

1. Z **souboru** klikněte na nabídku **nový projekt**.
2. V **nový projekt** dialogového okna rozbalte **jazyka C#** pod **šablony** a vyberte **webové**.
3. Vyberte **prázdná webová aplikace ASP.NET** šablony, pojmenujte projekt *SignalR.StockTicker*a klikněte na tlačítko **OK**.

    ![Dialogové okno Nový projekt](tutorial-server-broadcast-with-aspnet-signalr/_static/image2.png)

<a id="nugetpackages"></a>

## <a name="add-the-signalr-nuget-packages"></a>Přidání balíčků SignalR NuGet

### <a name="add-the-signalr-and-jquery-nuget-packages"></a>Přidat funkci SignalR a balíčky JQuery NuGet

Funkce SignalR můžete přidat do projektu po instalaci balíčku NuGet.

1. Klikněte na tlačítko **nástroje | Správce balíčků NuGet | Konzola správce balíčků**.
2. Správce balíčků zadejte následující příkaz.

    [!code-powershell[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample1.ps1)]

    Funkce SignalR balíček nainstaluje celou řadou dalších balíčcích NuGet jako závislosti. Po dokončení instalace budete mít vše serveru a klientské komponenty potřebné k použití v aplikaci ASP.NET SignalR.

<a id="server"></a>

## <a name="set-up-the-server-code"></a>Nastavte si do kódu serveru

V této části můžete nastavit kód, který běží na serveru.

### <a name="create-the-stock-class"></a>Vytvořte třídu akcií

Začnete vytvořením třídy akcie modelu, které budete používat k ukládání a přenášení informací o stejných akcií.

1. Vytvořte nový soubor třídy do složky projektu, pojmenujte ho *Stock.cs*a potom nahraďte kód šablony následujícím kódem:

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample2.cs)]

    Dvě vlastnosti, které nastavíte při vytváření akcie se symboly (například MSFT pro Microsoft) a ceny. Ostatní vlastnosti závisí na kdy a jak nastavit cena. Při prvním nastavení cen, hodnota získá rozšíří na DayOpen. Následující časy při nastavení cen, změny a PercentChange hodnoty vlastností se počítají podle rozdíl mezi cenou a DayOpen.

### <a name="create-the-stockticker-and-stocktickerhub-classes"></a>Vytvoření tříd StockTicker a StockTickerHub

Rozhraní API pro rozbočovače SignalR budete používat ke zpracování server klient interakce. StockTickerHub třídu odvozenou z třídy rozbočovače SignalR zpracuje, připojení a volání metody přijímají od klientů. Potřebujete také udržovat uložených dat a spuštění časovače objekt pravidelně aktivovat aktualizaci cen, nezávisle na připojení klientů. Tyto funkce nelze vložit ve třídě centra vzhledem k tomu, že jsou přechodné instance rozbočovače. Pro každou operaci v rozbočovači, jako je například připojení a volání od klienta k serveru se vytvoří instance třídy rozbočovače. Mechanismus, který zajišťuje uložených dat, aktualizuje ceny a vysílá aktualizaci cen má ke spuštění v samostatné třídě, která bude název StockTicker.

![Všesměrové vysílání z StockTicker](tutorial-server-broadcast-with-aspnet-signalr/_static/image4.png)

Chcete pouze jedna instance třídy StockTicker ke spuštění na serveru, takže budete muset nastavit odkaz z každé instance StockTickerHub StockTicker instanci typu singleton. Třída StockTicker musí umět vysílat pro klienty, protože má uložených dat a aktivuje aktualizace, ale StockTicker není třída rozbočovače. Proto má třída StockTicker k získání odkazu na objekt kontextu připojení rozbočovače SignalR. Pak můžete objekt context připojení SignalR na klienty.

1. V **Průzkumníka řešení**, klikněte pravým tlačítkem na projekt a klikněte na tlačítko **přidat novou položku**.
2. Pokud máte Visual Studio 2012 s [technologie ASP.NET a Web Tools 2012.2 Update](https://go.microsoft.com/fwlink/?LinkId=279941), klikněte na tlačítko **webové** pod **Visual C#** a vyberte **třída rozbočovače SignalR** šablony položky. Další možností je vybrat **třídy** šablony.
3. Pojmenujte novou třídu *StockTickerHub.cs*a potom klikněte na tlačítko **přidat**.

    ![Add StockTickerHub.cs](tutorial-server-broadcast-with-aspnet-signalr/_static/image5.png)
4. Nahraďte kód šablony následujícím kódem:

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample3.cs)]

    [Centra](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx) třída se používá k definování metody klienty můžete volat na serveru. Definujete jednu metodu: `GetAllStocks()`. Když klient se nejprve připojí k serveru, bude volat tuto metodu za účelem získání seznamu všech zásob s jejich aktuální ceny. Metoda může provést synchronně a vrátit `IEnumerable<Stock>` vzhledem k tomu, že ji vrací data z paměti. Pokud má metodu k získání dat tímto způsobem něco, co by vyžadovalo čekání, jako je například vyhledávání v databázi nebo volání webové služby, zadali byste `Task<IEnumerable<Stock>>` jako návratovou hodnotu k povolení asynchronního zpracování. Další informace najdete v tématu [ASP.NET pokyny k rozhraní API Center SignalR - Server - kdy spustit asynchronně](index.md).

    HubName atribut určuje, jak se bude odkazovat centrum v kódu jazyka JavaScript na straně klienta. Výchozí název na straně klienta, pokud nepoužijete tento atribut je verze název třídy, kterou v tomto případě by stockTickerHub-ve formátu camelCase.

    Jak uvidíte později při vytváření třídy StockTicker, se vytvoří instanci typu singleton této třídy v jeho statickou vlastnost Instance. Instanci typu singleton StockTicker zůstanou v paměti bez ohledu na to, kolik klientů připojovat nebo odpojovat, a tato instance je metoda GetAllStocks používá k vrácení aktuální základní informace o.
5. Vytvořte nový soubor třídy do složky projektu, pojmenujte ho *StockTicker.cs*a potom nahraďte kód šablony následujícím kódem:

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample4.cs)]

    Protože více vláken používat stejnou instanci StockTicker kódu, musí být threadsafe StockTicker třídy.

    ### <a name="storing-the-singleton-instance-in-a-static-field"></a>Instanci typu singleton ukládání do statických polí

    Kód inicializuje statické \_pole instance, která zálohuje vlastnost Instance s instancí třídy, a to je jedinou instanci třídy, která mohou být vytvořeny, protože konstruktor je označený jako privátní. [Opožděná inicializace](https://msdn.microsoft.com/library/dd997286.aspx) se používá pro \_pole instance, není kvůli výkonu ale pokud chcete zajistit, že vytvoření instance threadsafe.

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample5.cs)]

    Pokaždé, když klient připojí k serveru, novou instanci třídy StockTickerHub spuštěna v samostatném vlákně získává instanci typu singleton StockTicker z StockTicker.Instance statické vlastnosti, kterou jste předtím viděli StockTickerHub třídy.

    ### <a name="storing-stock-data-in-a-concurrentdictionary"></a>Ukládání dat uložených v ConcurrentDictionary

    Konstruktor inicializuje \_akcie kolekce s určitými ukázkových uložených dat a GetAllStocks vrátí zásob. Jak jste viděli již dříve, je této kolekce akcie zase vrácený StockTickerHub.GetAllStocks, což je metoda serveru ve třídě rozbočovače, který klienti mohou volat.

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample6.cs)]

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample7.cs)]

    Kolekce akcie je definován jako [ConcurrentDictionary](https://msdn.microsoft.com/library/dd287191.aspx) typ pro bezpečný přístup z více vláken. Jako alternativu můžete použít [slovníku](https://msdn.microsoft.com/library/xfhwa508.aspx) objektu a explicitně zamknout slovníku, když provedete změny.

    V této ukázkové aplikaci je OK k ukládání dat aplikací v paměti a ke ztrátě dat při uvolnění StockTicker instance. V reálné aplikaci když pracujete s back endovým datům úložiště, například do databáze.

    ### <a name="periodically-updating-stock-prices"></a>Pravidelně aktualizuje cenami akcií

    Konstruktor spuštění objekt časovače, která pravidelně volá metody, které aktualizují cenami akcií v náhodných intervalech.

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample8.cs)]

    UpdateStockPrices je volán časovač, který předá hodnotu null v parametru state. Před aktualizací ceny, je pořízené Zámek \_updateStockPricesLock objektu. Kód zkontroluje, zda jiné vlákno se už aktualizuje ceny, a pak zavolá TryUpdateStockPrice na každé populace v seznamu. Metoda TryUpdateStockPrice rozhodne, zda se má změnit akcií a kolik ho změnit. Pokud se změní minimální cenu akcie BroadcastStockPrice je volána k vysílání změnit minimální cenu akcie pro všechny připojené klienty.

    \_UpdatingStockPrices příznak je označen jako [volatile](https://msdn.microsoft.com/library/x13ttww7.aspx) tak, aby byl přístup k němu threadsafe.

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample9.cs)]

    V reálné aplikaci by metoda TryUpdateStockPrice volání webové služby k vyhledání ceny; Tento kód použije generátor náhodných čísel náhodně provádět změny.

    ### <a name="getting-the-signalr-context-so-that-the-stockticker-class-can-broadcast-to-clients"></a>Získávání kontextu SignalR tak, aby třída StockTicker můžete vysílat pro klienty

    Protože změny cen pocházejí z objektu StockTicker tady, jedná se o objekt, který je potřeba zavolat metodu updateStockPrice na všechny připojené klienty. Ve třídě rozbočovače máte rozhraní API pro volání metody klienta, ale StockTicker nedědí ze třídy rozbočovače a nemá odkaz na libovolný objekt rozbočovače. Proto aby bylo možné vysílání připojeným klientům, StockTicker třídy musí získat instance kontextu SignalR pro třídu StockTickerHub, který budete používat pro volání metod na klientských počítačích.

    Kód získá odkaz na kontext SignalR při vytváření instance třídy singleton, předá, které odkazují na konstruktoru, a umístí jej konstruktoru vlastnost klientů.

    Existují dva důvody, proč chcete přijímat pouze jednou kontextu: získání kontextu je náročná operace a jednou pro spolupráci se zajistí zachování zamýšleném pořadí zpráv odeslaných do klientů.

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample10.cs)]

    Získání vlastnosti klienti kontextu a umístit ho do vlastnost StockTickerClient umožňuje napsat kód pro volání metody klienta, která vypadá stejně jako by tomu bylo v třídě rozbočovače. Například na všechny klienty můžete napsat Clients.All.updateStockPrice(stock).

    Metoda updateStockPrice, který voláte v BroadcastStockPrice ještě; neexistuje přidáte je později při psaní kódu, který běží na straně klienta. Najdete zde updateStockPrice protože Clients.All je dynamická, což znamená, že výraz se vyhodnotí za běhu. Při volání této metody se spustí, SignalR pošle názvu metody a hodnota parametru klienta a pokud klient má metodu s názvem updateStockPrice, zavolá tato metoda a hodnota parametru se předají do ní.

    Clients.All znamená, že odesílání pro všechny klienty. Funkce SignalR poskytuje další možnosti k určení, které klienti nebo skupiny klientů k odeslání. Další informace najdete v tématu [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx).

### <a name="register-the-signalr-route"></a>Zaregistrujte směrování funkce SignalR

Server musí znát adresu URL, která je pro zachycení a přístupem k systému SignalR. Provedete to, že přidáte kód, který *Global.asax* souboru.

1. V **Průzkumníka řešení**, klikněte pravým tlačítkem na projekt a potom klikněte na tlačítko **přidat novou položku**.
2. Vyberte **Global Application Class** šablony položky a pak klikněte na tlačítko **přidat**.

    ![Add global.asax](tutorial-server-broadcast-with-aspnet-signalr/_static/image6.png)
3. Přidat do aplikace kód SignalR postupu registrace\_začátek metody:

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample11.cs)]

    Ve výchozím nastavení, je základní adresu URL pro veškerý provoz SignalR "/ signalr", a "/ signalr/hubs" slouží k načtení dynamicky generovaný soubor jazyka JavaScript, který definuje proxy pro všechna centra máte ve své aplikaci. Metoda MapHubs zahrnuje přetížení, která umožňují určit různé základní adresu URL a některé možnosti SignalR v instanci [HubConfiguration](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubconfiguration(v=vs.111).aspx) třídy.
4. Přidat sadu pomocí příkazu v horní části souboru:

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample12.cs)]
5. Uložte a zavřete *Global.asax* souboru a sestavte projekt.

Teď jste dokončili nastavení do kódu serveru. V další části budete nastavení klienta.

<a id="client"></a>

## <a name="set-up-the-client-code"></a>Nastavit kód klienta

1. Vytvořte nový soubor HTML ve složce projektu a pojmenujte ho *StockTicker.html*.
2. Nahraďte kód šablony následujícím kódem:

    [!code-html[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample13.html)]

    Kód HTML vytvoří tabulku s 5 sloupci, řádek záhlaví a řádek dat s jedinou buňku, která překlenuje všechny sloupce 5. Řádek dat se zobrazí "..." načítání"a bude se zobrazovat jenom krátkodobě při spuštění aplikace. Kód jazyka JavaScript se odebrat tento řádek a přidat v místě řádky s uložených dat načtených ze serveru.

    Značky skriptu zadat soubor skriptu jQuery, soubor skriptu core SignalR, soubor skriptu proxy SignalR a StockTicker soubor skriptu, který později vytvoříte. Soubor skriptu proxy SignalR, který určuje adresu URL "/ signalr/centra", generuje dynamicky a v tomto případě definuje metody proxy pro metody u třídy rozbočovače pro StockTickerHub.GetAllStocks. Pokud dáváte přednost, tento soubor JavaScript vygenerovat ručně pomocí [nástroje SignalR](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) a vytváření dynamického souborů ve volání metody MapHubs zakázat.
3. > [!IMPORTANT]
   > Ujistěte se, že odkazuje na soubor jazyka JavaScript v *StockTicker.html* jsou správné. To znamená, ujistěte se, že jQuery verze v vaši značku skriptu (v příkladu 1.8.2) je stejná jako verze jQuery ve vašem projektu *skripty* složky a ujistěte se, že verze SignalR v vaši značku skriptu je stejný jako funkce SignalR verze ve vašem projektu *skripty* složky. Změňte názvy souborů v značek skriptu, v případě potřeby.
4. V **Průzkumníka řešení**, klikněte pravým tlačítkem na *StockTicker.html*a potom klikněte na tlačítko **nastavit jako úvodní stránku**.
5. Vytvořte nový soubor JavaScript ve složce projektu s názvem *StockTicker.js*...
6. Nahraďte kód šablony následujícím kódem:

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample14.js)]

    $.connection odkazuje na proxy služby SignalR. Kód získá odkaz na proxy serveru pro třídu StockTickerHub a umístí jej do proměnné akcie. Název proxy serveru je název, který se nastavuje atribut [HubName]:

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample15.js)]

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample16.cs)]

    Po definování proměnné a funkce jsou poslední řádek kódu v souboru inicializuje připojení SignalR volání start funkce SignalR. Spuštění funkce asynchronně provede a vrátí [jQuery odloženo objekt](http://api.jquery.com/category/deferred-object/), což znamená, že může volat funkci Hotovo k určení funkce, která má být volána po dokončení asynchronní operace...

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample17.js)]

    Init – funkce volá funkci getAllStocks na serveru a používá informace, který server vrátí aktualizace základní tabulky. Všimněte si, že ve výchozím nastavení, budete muset použít ve formátu camelCase malá a velká písmena na straně klienta i název metody je – jazyka Pascal – na serveru. Pravidlo camel-velká a malá písmena platí pouze pro metody, ne objekty. Například můžete odkazovat na skladě. Symbol a akcie. Cena, ne stock.symbol nebo stock.price.

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample18.js)]

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample19.cs)]

    Pokud jste chtěli použít malých a velkých písmen pascal na straně klienta, nebo pokud jste chtěli použít název úplně jiné metody, vám může vylepšení centra metodu s atributem HubMethodName stejným způsobem upravena třídy rozbočovače s atributem HubName.

    V metodě inicializace kód HTML pro řádek tabulky se vytvoří pro každou skladový objekt přijatých ze serveru volání formatStock na formát vlastnosti skladový objekt a potom volala mohla nahradit (která je definovaná v horní části *StockTicker.js*) nahraďte zástupné symboly v proměnné rowTemplate hodnoty vlastností skladový objekt. Výsledného souboru HTML se pak připojí k základní tabulky.

    Volat funkci inicializace jejím předáním jako funkce zpětného volání, který se spustí po dokončení asynchronního spuštění funkce. Pokud jste volali init jako samostatný příkaz jazyka JavaScript po volání start, funkce by selhat, protože by spustit okamžitě bez čekání na spuštění funkce dokončete navazování připojení. Funkce init v takovém případě by se pokusil zavolat funkci getAllStocks před navázáním připojení k serveru.

    Když na serveru změní cena akcie společnosti, volá updateStockPrice na připojené klienty. Funkce je přidána do vlastnosti klienta stockTicker proxy je k dispozici k volání ze serveru.

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample20.js)]

    Funkce updateStockPrice formátuje skladový objekt přijatou ze serveru do řádku tabulky na stejném principu funkce init. Místo přidávání řádku do tabulky, je však najde skladě aktuální řádek v tabulce a nahradí řádku novou.

<a id="test"></a>

## <a name="test-the-application"></a>Testování aplikace

1. Stisknutím klávesy F5 spusťte aplikaci v režimu ladění.

    Základní tabulky zpočátku zobrazí "načítání..." řádku, pak po krátké prodlevě, které se zobrazí počáteční uložených dat a spusťte ceny akcií, chcete-li změnit.

    ![Načítání](tutorial-server-broadcast-with-aspnet-signalr/_static/image7.png)

    ![Počáteční základní tabulka](tutorial-server-broadcast-with-aspnet-signalr/_static/image8.png)

    ![Základní tabulka přijímat změny ze serveru](tutorial-server-broadcast-with-aspnet-signalr/_static/image9.png)
2. Zkopírujte adresu URL z adresního řádku prohlížeče a vložte ho do jednoho nebo více nového okna prohlížeče.

    Počáteční uložených zobrazení je stejný jako první prohlížeče a změny probíhají souběžně.
3. Zavřít všechny prohlížeče a otevřete nový prohlížeč a přejděte na stejnou adresu URL.

    Objekt typu singleton StockTicker pokračuje ke spuštění na serveru, takže zobrazení základní tabulka ukazuje, že zásoby zlepšovalo, chcete-li změnit. (Nevidíte počáteční tabulka s nulou změnit hodnoty.)
4. Zavřete prohlížeč.

<a id="enablelogging"></a>

## <a name="enable-logging"></a>Povolit protokolování

SignalR má vestavěné protokolování funkci, kterou můžete povolit na straně klienta na podporu při řešení potíží. V této části Povolit protokolování a podívejte se na příklady, které ukazují, jak protokoly, že jste které z následujících metod přenosu pomocí SignalR:

- [Protokoly Websocket](http://en.wikipedia.org/wiki/WebSocket)podporovaný IIS 8 a aktuální prohlížeče.
- [Události odeslané serverem](http://en.wikipedia.org/wiki/Server-sent_events)podporovaný prohlížečích než Internet Explorer.
- [Navždy rámec](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe)podporovaný aplikace Internet Explorer.
- [Dlouhý interval dotazování AJAX](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling)podporovaná ve všech prohlížečích.

Pro jakékoli dané připojení SignalR vybere nejlepší metody přenosu, které podporují server i klient.

1. Otevřít *StockTicker.js* a přidejte řádek kódu a povolení protokolování bezprostředně před kódem, který inicializuje připojení na konci souboru:

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample21.js)]
2. Stisknutím klávesy F5 spusťte projekt.
3. Otevřete okno vývojářských nástrojů v prohlížeči a vyberte v konzole naleznete v protokolech. Budete muset aktualizovat stránku, aby zobrazil protokoly vyjednávání přepravy pro nové připojení Signalr.

    Pokud používáte Internet Explorer 10 v systému Windows 8 (IIS 8), je způsob přepravy objekty Websocket.

    ![Konzola, IE 10 IIS 8](tutorial-server-broadcast-with-aspnet-signalr/_static/image10.png)

    Pokud používáte Internet Explorer 10 na Windows 7 (službu IIS 7.5), je způsob přepravy iframe.

    ![IE 10 Console, IIS 7.5](tutorial-server-broadcast-with-aspnet-signalr/_static/image11.png)

    V aplikaci Firefox nainstalujte doplněk Firebug okno konzoly. Pokud používáte Firefox 19 ve Windows 8 (IIS 8), je přepravy objekty Websocket.

    ![Firefox 19 IIS 8 Websockets](tutorial-server-broadcast-with-aspnet-signalr/_static/image12.png)

    Pokud používáte Firefox 19 ve Windows 7 (službu IIS 7.5), je způsob přepravy události odeslané serverem.

    ![Konzola služby IIS 7.5, Firefox 19](tutorial-server-broadcast-with-aspnet-signalr/_static/image13.png)

<a id="fullsample"></a>

## <a name="install-and-review-the-full-stockticker-sample"></a>Instalace a zkontrolujte úplnou ukázku StockTicker

StockTicker aplikace, který je nainstalovaný [Microsoft.AspNet.SignalR.Sample](http://nuget.org/packages/microsoft.aspnet.signalr.sample) balíček NuGet obsahuje víc funkcí než zjednodušenou verzi, kterou jste právě vytvořili úplně od začátku. V této části kurzu nainstalujte balíček NuGet a projděte si nové funkce a kód, který je implementuje.

### <a name="install-the-signalrsample-nuget-package"></a>Nainstalujte balíček SignalR.Sample NuGet

1. V **Průzkumníka řešení**, klikněte pravým tlačítkem na projekt a klikněte na tlačítko **spravovat balíčky NuGet**.
2. V **spravovat balíčky NuGet** dialogové okno, klikněte na tlačítko **Online**, zadejte *SignalR.Sample* v **vyhledávání Online** pole a potom klikněte na tlačítko  **Nainstalujte** v **SignalR.Sample** balíčku.

    ![Nainstalujte balíček SignalR.Sample](tutorial-server-broadcast-with-aspnet-signalr/_static/image14.png)
3. V *Global.asax* souboru, Odkomentujte RouteTable.Routes.MapHubs(); řádek, že jste přidali dříve v aplikaci\_začátek metody.

    Kód v *Global.asax* je už nepotřebujete, protože balíček SignalR.Sample zaregistruje trasu SignalR v *aplikace\_Start/RegisterHubs.cs* souboru:

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample22.cs)]

    Třída WebActivator, na který odkazuje atribut sestavení je součástí balíčku WebActivatorEx NuGet, který je nainstalován jako závislost balíčku SignalR.Sample.
4. V **Průzkumníka řešení**, rozbalte *SignalR.Sample* složky, který byl vytvořen při instalaci balíčku SignalR.Sample.
5. V *SignalR.Sample* složky, klikněte pravým tlačítkem na *StockTicker.html*a potom klikněte na tlačítko **nastavit jako úvodní stránku**.

    > [!NOTE]
    > Instalace SignalR.Sample NuGet balíčku může změnit verzi jQuery, který máte v vaše *skripty* složky. Nové *StockTicker.html* soubor, který se nainstaluje balíček *SignalR.Sample* složkou je synchronizovaný s verzí jQuery, který nainstaluje balíček, ale pokud budete chtít spustit váš původním *StockTicker.html* soubor znovu, možná budete muset nejprve aktualizovat odkaz jQuery ve značce skriptu.

### <a name="run-the-application"></a>Spuštění aplikace

1. Stisknutím klávesy F5 spusťte aplikaci.

    Kromě mřížky, které jste viděli dříve úplné akciích aplikace ukazuje vodorovně posuvné okno, které se zobrazí stejná základní data. Když spustíte aplikaci poprvé, "trhu" je "uzavřený" a uvidíte statické mřížky a akcie okna, který není posouvání.

    ![StockTicker obrazovky start](tutorial-server-broadcast-with-aspnet-signalr/_static/image15.png)

    Po kliknutí na **otevřeném trhu**, **Live akcie akcie** pole začne posouvat vodorovně a spustí se server pravidelně vysílat změny ceny akcie v náhodných intervalech. Pokaždé, když ceny akcie změní, i **Live tabulky akcie** mřížky a **Live akcie akcie** pole jsou aktualizovány. Pokud je změna ceny akcie společnosti kladná, stock je zobrazen zeleně na pozadí a při změně je záporný, stock se zobrazí s červeným pozadím.

    ![Otevřete aplikaci StockTicker trhu](tutorial-server-broadcast-with-aspnet-signalr/_static/image16.png)

    **Zavřít trhu** tlačítko přestane změny a posouvání akcií, k dispozici a **resetování** tlačítko obnoví všechny uložených dat do původního stavu před zahájením změny cen. Pokud otevřete další okno prohlížeče a přejděte na stejnou adresu URL, uvidíte stejná data dynamicky aktualizovat ve stejnou dobu v každým prohlížečem. Po klepnutí na tlačítka, reagujte všechny prohlížeče stejným způsobem jako ve stejnou dobu.

### <a name="live-stock-ticker-display"></a>Živé akcie časovače, může zobrazení

**Live akcie akcie** zobrazení je neuspořádaný seznam do elementu div, který je formátován jako jeden řádek pomocí stylů CSS. Časovače, může je inicializován a aktualizovat stejným způsobem jako v tabulce: tak, že nahradíte zástupný text v &lt;li&gt; řetězec šablony a dynamicky přidat &lt;li&gt; prvků, které mají &lt;ul&gt; element. Posouvání se provádí pomocí funkce animovat jQuery se liší okraj levé neuspořádaný seznam v rámci div.

Akciích HTML:

[!code-html[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample23.html)]

Akciích šablon stylů CSS:

[!code-html[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample24.html)]

Posuňte se kód jazyka jQuery, která umožňuje:

[!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample25.js)]

### <a name="additional-methods-on-the-server-that-the-client-can-call"></a>Další metody na serveru, na které můžete volat klienta

Třída StockTickerHub definuje čtyři další metody, které můžete volat klienta:

[!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample26.cs)]

V reakci na tlačítka v horní části stránky se nazývají OpenMarket CloseMarket a obnovení. Vysvětlují vzor jednoho klienta, spouštění změnu stavu, ve kterém se okamžitě šíří do všech klientů. Každá z těchto metod volá metodu ve třídě StockTicker který postihne trhu stav změnit a pak vyšle nový stav.

Ve třídě StockTicker udržuje MarketState vlastnost, která vrací hodnotu výčtu MarketState stavu na trhu:

[!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample27.cs)]

Každá z metod, které ke změně stavu na trhu provést uvnitř bloku zámek protože StockTicker třída musí být threadsafe:

[!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample28.cs)]

K zajištění, že tento kód je threadsafe, \_marketState pole, která zálohuje MarketState vlastnost je označena jako volatile,

[!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample29.cs)]

Metody BroadcastMarketStateChange a BroadcastMarketReset jsou podobné BroadcastStockPrice metody, které jste už viděli, s výjimkou volání různých metod definovaných v klientském počítači:

[!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample30.cs)]

### <a name="additional-functions-on-the-client-that-the-server-can-call"></a>Další funkce na straně klienta, která může volat na serveru

Funkce updateStockPrice nyní zpracovává mřížky a časovače, může zobrazení a používá jQuery.Color pro flash červenou a zelenou barvy.

Nové funkce v *SignalR.StockTicker.js* povolit a zakázat tlačítka na základě trhu stavu a zastavení nebo spuštění časovače, může okno vodorovného posouvání. Vzhledem k tomu, že na ticker.client, se neustále přidávají více funkcí [jQuery rozšířit funkce](http://api.jquery.com/jQuery.extend/) se používá k přidání je.

[!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample31.js)]

### <a name="additional-client-setup-after-establishing-the-connection"></a>Instalace dalších klientských po navázání připojení

Poté, co klient naváže připojení, je provést další úkony: Zjistěte, jestli je otevřeno nebo zavřeno, aby bylo možné volat odpovídající marketOpened nebo marketClosed funkce a volání metody serveru pro tlačítka připojit na trhu.

[!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample32.js)]

Metody serveru nejsou svázanou tlačítka až po navázání připojení tak, aby kód pokusí volat metody serveru, dokud nebudou k dispozici.

<a id="nextsteps"></a>

## <a name="next-steps"></a>Další kroky

V tomto kurzu jste zjistili, jak programovat aplikace SignalR, který vysílá zprávy ze serveru na všechny připojené klienty, a v pravidelných intervalech a v reakci na oznámení z jakéhokoli klienta. Vzor pomocí instance typu singleton vícevláknové k údržbě stavu serveru také lze také v online her scénáře více hráčů. Příklad najdete v tématu [ShootR hru, která je založena na SignalR](https://github.com/NTaylorMullen/ShootR).

Kurzy, které ukazují scénáře komunikace peer-to-peer, naleznete v tématu [Začínáme s knihovnou SignalR](index.md) a [aktualizace v reálném čase s knihovnou SignalR](index.md).

Informace o pokročilejších pojmech vývoj SignalR, naleznete na následujících stránkách pro funkci SignalR zdrojový kód a prostředky:

- [Funkce SignalR technologie ASP.NET](https://asp.net/signalr/)
- [Projekt SignalR](http://signalr.net/)
- [Funkce SignalR Githubu a ukázky](https://github.com/SignalR/SignalR)
- [SignalR Wiki](https://github.com/SignalR/SignalR/wiki)
