---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-javascript-client
title: ASP.NET SignalR Hubs API Guide - JavaScript Client | Dokumenty společnosti Microsoft
author: bradygaster
description: Tento dokument poskytuje úvod do používání rozhraní HUBS API pro SignalR verze 2 v klientech JavaScriptu, jako jsou prohlížeče a aplikátor Windows Store (WinJS) ...
ms.author: bradyg
ms.date: 01/15/2019
ms.assetid: a9fd4dc0-1b96-4443-82ca-932a5b4a8ea4
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-javascript-client
msc.type: authoredcontent
ms.openlocfilehash: 8befe133c3627dac1f7d011959c68e2054d345da
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676081"
---
# <a name="aspnet-signalr-hubs-api-guide---javascript-client"></a>ASP.NET SignalR Hubs API Guide - JavaScript Client

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Tento dokument poskytuje úvod do používání rozhraní HUBS API pro SignalR verze 2 v klientech JavaScriptu, jako jsou prohlížeče a aplikace Windows Store (WinJS).
>
> Rozhraní API signalr hubs umožňuje provádět vzdálená volání procedur (RPC) ze serveru do připojených klientů a z klientů na server. V kódu serveru definujete metody, které mohou být volány klienty, a volání metod, které jsou spuštěny na straně klienta. V klientském kódu definujete metody, které lze volat ze serveru, a volání metod, které jsou spuštěny na serveru. SignalR se postará o všechny klient-to-server instalatérské pro vás.
>
> SignalR také nabízí rozhraní API nižší úrovně s názvem Trvalá připojení. Úvod k SignalR, rozbočovače a trvalá připojení naleznete [v tématu Úvod do SignalR](../getting-started/introduction-to-signalr.md).
>
> ## <a name="software-versions-used-in-this-topic"></a>Verze softwaru použité v tomto tématu
>
>
> - [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)
> - .NET 4.5
> - SignalR verze 2
>
>
>
> ## <a name="previous-versions-of-this-topic"></a>Předchozí verze tohoto tématu
>
> Informace o dřívějších verzích SignalR naleznete v tématu [SignalR Older Versions](../older-versions/index.md).
>
> ## <a name="questions-and-comments"></a>Dotazy a připomínky
>
> Prosím, zanechte zpětnou vazbu o tom, jak se vám líbil tento výukový program a co bychom mohli zlepšit v komentářích v dolní části stránky. Máte-li otázky, které nejsou přímo spojeny s tutoriálu, můžete je odeslat do [fóra ASP.NET SignalR](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) nebo [StackOverflow.com](http://stackoverflow.com/).

## <a name="overview"></a>Přehled

Tento dokument obsahuje následující části:

- [Vygenerovaný proxy server a co to dělá pro vás](#genproxy)

    - [Kdy použít vygenerovaný proxy server](#cantusegenproxy)
- [Nastavení klienta](#clientsetup)

    - [Jak odkazovat na dynamicky generovaný proxy server](#dynamicproxy)
    - [Jak vytvořit fyzický soubor pro proxy server vygenerovaný signalr](#manualproxy)
- [Jak navázat spojení](#establishconnection)

    - [$.connection.hub je stejný objekt, který vytvoří $.hubConnection()](#connequivalence)
    - [Asynchronní spuštění metody start](#asyncstart)
- [Jak navázat připojení mezi doménami](#crossdomain)
- [Jak nakonfigurovat připojení](#configureconnection)

    - [Jak zadat parametry řetězce dotazu](#querystring)
    - [Jak určit způsob přenosu](#transport)
- [Jak získat proxy pro třídu Hub](#getproxy)
- [Jak definovat metody na straně klienta, který může server volat](#callclient)
- [Jak volat metody serveru z klienta](#callserver)
- [Jak zpracovat události životnosti připojení](#connectionlifetime)
- [Jak zpracovat chyby](#handleerrors)
- [Jak povolit protokolování na straně klienta](#logging)

Dokumentaci k programování serveru nebo klientů .NET naleznete v následujících zdrojích informací:

- [Průvodce rozhraním API hubů SignalR – server](hubs-api-guide-server.md)
- [Průvodce rozhraním API hubů SignalR – klient .NET](hubs-api-guide-net-client.md)

Součást serveru SignalR 2 je k dispozici pouze v rozhraní .NET 4.5 (i když je klient .NET pro SignalR 2 na rozhraní .NET 4.0).

<a id="genproxy"></a>

## <a name="the-generated-proxy-and-what-it-does-for-you"></a>Vygenerovaný proxy server a co to dělá pro vás

Můžete naprogramovat klienta JavaScript u společnosti SignalR se službou SignalR nebo bez něj, který pro vás signalr generuje. Co proxy dělá pro vás je zjednodušit syntaxi kódu, který používáte pro připojení, psát metody, které server volá, a metody volání na serveru.

Při psaní kódu pro volání serverových metod umožňuje vygenerovaný proxy server použít syntaxi, `serverMethod(arg1, arg2)` která `invoke('serverMethod', arg1, arg2)`vypadá, jako byste prováděli místní funkci: můžete místo . Vygenerovaná syntaxe proxy také umožňuje okamžitou a srozumitelnou chybu na straně klienta, pokud nesprávně zadáte název metody serveru. A pokud ručně vytvoříte soubor, který definuje proxy servery, můžete také získat podporu IntelliSense pro psaní kódu, který volá metody serveru.

Předpokládejme například, že máte na serveru následující třídu Hub:

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample1.cs?highlight=1,3,5)]

Následující příklady kódu ukazují, jak vypadá kód JavaScript `NewContosoChatMessage` u vyvolání metody na serveru `addContosoChatMessageToPage` a přijímání vyvolání metody ze serveru.

**S vygenerovaným proxy**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample2.js?highlight=1-2,8)]

**Bez generovaného proxy**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample3.js?highlight=2-3,9)]

<a id="cantusegenproxy"></a>

### <a name="when-to-use-the-generated-proxy"></a>Kdy použít vygenerovaný proxy server

Pokud chcete zaregistrovat více obslužných rutin událostí pro klientskou metodu, kterou server volá, nemůžete použít vygenerovaný proxy server. V opačném případě můžete použít vygenerovaný proxy server nebo ne na základě předvoleb kódování. Pokud se rozhodnete ji nepoužívat, nemusíte odkazovat na adresu URL "signalr/hubs" v `script` prvku ve vašem klientském kódu.

<a id="clientsetup"></a>

## <a name="client-setup"></a>Nastavení klienta

Klient JavaScriptu vyžaduje odkazy na jQuery a základní javascriptový soubor SignalR. Verze jQuery musí být 1.6.4 nebo hlavní novější verze, například 1.7.2, 1.8.2 nebo 1.9.1. Pokud se rozhodnete použít vygenerovaný proxy server, budete také potřebovat odkaz na signalr generovaný proxy JavaScript soubor. Následující příklad ukazuje, jak mohou odkazy vypadat na stránce HTML, která používá generovaný proxy server.

[!code-html[Main](hubs-api-guide-javascript-client/samples/sample4.html)]

Tyto odkazy musí být zahrnuty v tomto pořadí: jQuery first, SignalR core po tom a SignalR proxy naposledy.

<a id="dynamicproxy"></a>

### <a name="how-to-reference-the-dynamically-generated-proxy"></a>Jak odkazovat na dynamicky generovaný proxy server

V předchozím příkladu je odkaz na proxy server generovaný SignalR dynamicky generovaný kód Jazyka JavaScript, nikoli na fyzický soubor. SignalR vytvoří javascriptový kód pro proxy za běhu a slouží klientovi v reakci na adresu URL "/signalr/hubs". Pokud jste ve své `MapSignalR` metodě zadali jinou základní adresu URL pro připojení SignalR na serveru, je adresa URL dynamicky generovaného souboru proxy vaší vlastní adresou URL s připojenou "/hubs".

> [!NOTE]
> Pro klienty JavaScriptu pro Windows 8 (Windows Store) použijte fyzický soubor proxy namísto dynamicky generovaného. Další informace naleznete v [tématu Jak vytvořit fyzický soubor pro server proxy generovaný signalr](#manualproxy) dále v tomto tématu.

V zobrazení ASP.NET MVC 4 nebo 5 Razor použijte vlnovku k odkazování na kořen aplikace v odkazu na soubor proxy:

[!code-html[Main](hubs-api-guide-javascript-client/samples/sample5.html)]

Další informace o používání signalru v MVC 5 naleznete v [tématech Začínáme s signalrem a MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md).

V zobrazení ASP.NET MVC 3 `Url.Content` Razor použijte pro odkaz na proxy soubor:

[!code-cshtml[Main](hubs-api-guide-javascript-client/samples/sample6.cshtml)]

V aplikaci ASP.NET webových formulářů použijte `ResolveClientUrl` pro odkaz na soubor proxy servery nebo jej zaregistrujte pomocí správce skriptů pomocí relativní cesty kořenového adresáře aplikace (počínaje vlnovkou):

[!code-aspx[Main](hubs-api-guide-javascript-client/samples/sample7.aspx)]

Obecně platí, že použijte stejnou metodu pro určení adresy URL "/signalr/hubs", kterou používáte pro soubory CSS nebo JavaScript. Pokud zadáte adresu URL bez použití vlnovky, v některých scénářích bude aplikace fungovat správně při testování v sadě Visual Studio pomocí služby IIS Express, ale při nasazení do úplné služby IIS se nezdaří, ale při nasazení do úplné služby IIS se nezdaří chyba 404. Další informace naleznete **v tématu Řešení odkazů na prostředky kořenové úrovně** na [webových serverech v sadě Visual Studio pro ASP.NET webových projektech](https://msdn.microsoft.com/library/58wxa9w5.aspx) na webu MSDN.

Když spustíte webový projekt v Sadě Visual Studio 2017 v režimu ladění a pokud používáte Internet Explorer jako prohlížeč, můžete zobrazit soubor proxy v **Průzkumníku řešení** v části **Skripty**.

Chcete-li zobrazit obsah souboru, poklepejte na **rozbočovače**. Pokud nepoužíváte Visual Studio 2012 nebo 2013 a Internet Explorer, nebo pokud nejste v režimu ladění, můžete také získat obsah souboru procházením adresy URL "/signalR/hubs". Pokud je například web `http://localhost:56699`spuštěn v `http://localhost:56699/SignalR/hubs` aplikaci , přejděte do prohlížeče.

<a id="manualproxy"></a>

### <a name="how-to-create-a-physical-file-for-the-signalr-generated-proxy"></a>Jak vytvořit fyzický soubor pro proxy server vygenerovaný signalr

Jako alternativu k dynamicky generovanému proxy serveru můžete vytvořit fyzický soubor, který má proxy kód a odkaz na tento soubor. Můžete to udělat pro kontrolu nad ukládáním do mezipaměti nebo sdružováním chování, nebo získat IntelliSense při kódování volání serverové metody.

Chcete-li vytvořit soubor proxy, proveďte následující kroky:

1. Nainstalujte balíček [Microsoft.AspNet.SignalR.Utils](https://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) NuGet.
2. Otevřete příkazový řádek a vyhledejte složku *nástrojů,* která obsahuje soubor SignalR.exe. Složka nástroje je v následujícím umístění:

    `[your solution folder]\packages\Microsoft.AspNet.SignalR.Utils.2.1.0\tools`
3. Zadejte následující příkaz:

    `signalr ghp /path:[path to the .dll that contains your Hub class]`

    Cesta k *dll je* obvykle složka *bin* ve složce projektu.

    Tento příkaz vytvoří soubor s názvem *server.js* ve stejné složce jako *signalr.exe*.
4. Vložte soubor *server.js* do příslušné složky v projektu, přejmenujte jej podle potřeby pro vaši aplikaci a přidejte na něj odkaz namísto odkazu signala/hubs.

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a>Jak navázat spojení

Před navázáním připojení je třeba vytvořit objekt připojení, vytvořit proxy server a zaregistrovat obslužné rutiny událostí pro metody, které lze volat ze serveru. Když jsou nastaveny proxy servery a obslužné rutiny událostí, navázat připojení voláním `start` metody.

Pokud používáte vygenerovaný proxy server, nemusíte vytvářet objekt připojení ve vlastním kódu, protože generovaný proxy kód to udělá za vás.

<a id="nogenconnection"></a>

**Navázat spojení (s vygenerovaným proxy serverem)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample8.js?highlight=5)]

**Navázat spojení (bez generovaného proxy serveru)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample9.js?highlight=1,6)]

Ukázkový kód používá výchozí adresu URL "/signalr" pro připojení ke službě SignalR. Informace o tom, jak zadat jinou základní adresu URL, naleznete [v tématu ASP.NET SignalR Hubs API Guide - Server - Adresa URL /signalr](hubs-api-guide-server.md#signalrurl).

Ve výchozím nastavení je umístění rozbočovače aktuální mstou. Pokud se připojujete k jinému serveru, zadejte adresu URL před voláním `start` metody, jak je znázorněno v následujícím příkladu:

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample10.js)]

> [!NOTE]
> Obvykle zaregistrujete obslužné rutiny událostí před voláním `start` metody k navázání připojení. Pokud chcete zaregistrovat některé obslužné rutiny událostí po navázání připojení, můžete to udělat, ale `start` musíte zaregistrovat alespoň jednu z obslužné rutiny událostí před voláním metody. Jedním z důvodů je, že v aplikaci může být mnoho center, `OnConnected` ale nebudete chtít spustit událost v každém centru, pokud budete používat pouze pro jednu z nich. Při navázání připojení, přítomnost metody klienta na proxy hubu je to, `OnConnected` co říká SignalR ke spuštění události. Pokud nezaregistrujete žádné obslužné rutiny událostí před voláním `start` metody, budete moci `OnConnected` vyvolat metody v centru, ale metoda Centra nebude volána a ze serveru nebudou vyvolány žádné klientské metody.

<a id="connequivalence"></a>

### <a name="connectionhub-is-the-same-object-that-hubconnection-creates"></a>$.connection.hub je stejný objekt, který vytvoří $.hubConnection()

Jak můžete vidět z příkladů, při použití generovanéproxy, `$.connection.hub` odkazuje na objekt připojení. Jedná se o stejný objekt, `$.hubConnection()` který získáte voláním, když nepoužíváte vygenerovaný proxy server. Generovaný proxy kód vytvoří připojení pro vás provedením následujícího příkazu:

![Vytvoření připojení v generovaném souboru proxy](hubs-api-guide-javascript-client/_static/image3.png)

Pokud používáte vygenerovaný proxy server, `$.connection.hub` můžete dělat cokoliv s tím, co můžete dělat s objektem připojení, když nepoužíváte generovaný proxy server.

<a id="asyncstart"></a>

### <a name="asynchronous-execution-of-the-start-method"></a>Asynchronní spuštění metody start

Metoda `start` se provádí asynchronně. Vrátí [jQuery Odložené objektu](http://api.jquery.com/category/deferred-object/), což znamená, že můžete přidat `pipe` `done`funkce `fail`zpětného volání voláním metody, jako je například , a . Pokud máte kód, který chcete spustit po navázání připojení, jako je například volání metody serveru, vložte tento kód do funkce zpětného volání nebo jej volejte z funkce zpětného volání. Metoda `.done` zpětného volání je spuštěna po navázání připojení a po `OnConnected` spuštění kódu, který máte v metodě obslužné rutiny události na serveru.

Pokud vložíte příkaz "Nyní připojeno" z předchozího příkladu `start` jako další řádek `.done` kódu za `console.log` volání metody (není v zpětném volání), řádek se spustí před navázáním připojení, jak je znázorněno v následujícím příkladu:

![Nesprávný způsob psaní kódu, který se spustí po navázání připojení](hubs-api-guide-javascript-client/_static/image5.png)

<a id="crossdomain"></a>

## <a name="how-to-establish-a-cross-domain-connection"></a>Jak navázat připojení mezi doménami

Obvykle, pokud prohlížeč načte `http://contoso.com`stránku z , signalr připojení `http://contoso.com/signalr`je ve stejné doméně, at . Pokud stránka `http://contoso.com` z vytvoří `http://fabrikam.com/signalr`připojení k , to je připojení mezi doménami. Z bezpečnostních důvodů jsou připojení mezi doménami ve výchozím nastavení zakázána.

V SignalR 1.x byly požadavky mezi doménami řízeny jedním příznakem EnableCrossDomain. Tento příznak řídil požadavky JSONP i CORS. Pro větší flexibilitu byla veškerá podpora CORS odebrána ze serverové součásti SignalR (javascriptoví klienti stále používají CORS normálně, pokud je zjištěno, že prohlížeč podporuje) a pro podporu těchto scénářů byl zpřístupněn nový middleware OWIN.

Pokud je jsonp požadován o klientovi (pro podporu požadavků napříč doménami ve `EnableJSONP` starších `HubConfiguration` prohlížečích), bude nutné jej explicitně povolit nastavením objektu na `true`, jak je znázorněno níže. JSONP je ve výchozím nastavení zakázán, protože je méně bezpečný než CORS.

**Přidání microsoft.owin.cors do projektu:** Chcete-li nainstalovat tuto knihovnu, spusťte v konzole Správce balíčků následující příkaz:

`Install-Package Microsoft.Owin.Cors`

Tento příkaz přidá verzi balíčku 2.1.0 do projektu.

### <a name="calling-usecors"></a>Volání UseCors

 Následující fragment kódu ukazuje, jak implementovat připojení mezi doménami v SignalR 2.

**Implementace požadavků mezi doménami v SignalR 2**

Následující kód ukazuje, jak povolit CORS nebo JSONP v projektu SignalR 2. Tato ukázka `Map` `RunSignalR` kódu `MapSignalR`používá a místo , tak, aby middleware CORS běží pouze pro požadavky SignalR, které `MapSignalR`vyžadují podporu CORS (spíše než pro všechny provozy na cestě určené v .) Mapa může být také použita pro jakýkoli jiný middleware, který potřebuje ke spuštění pro konkrétní předponu URL, spíše než pro celou aplikaci.

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample11.cs)]

> [!NOTE]
>
> - Nenastavujte `jQuery.support.cors` hodnotu true v kódu.
>
>     ![Nenastavovat jQuery.support.cors na true](hubs-api-guide-javascript-client/_static/image7.png)
>
>     SignalR zpracovává použití CORS. Nastavení `jQuery.support.cors` true zakáže JSONP, protože způsobí, že SignalR předpokládat, že prohlížeč podporuje CORS.
> - Pokud se připojujete k adrese URL localhost, aplikace Internet Explorer 10 to nebude považovat za připojení mezi doménami, takže aplikace bude pracovat místně s aplikací IE 10, i když jste na serveru nepovolili připojení mezi doménami.
> - Informace o používání připojení mezi doménami v aplikaci Internet Explorer 9 naleznete v [tomto vlákně StackOverflow](http://stackoverflow.com/questions/13573397/siganlr-ie9-cross-domain-request-dont-work).
> - Informace o používání připojení mezi doménami v Chromu naleznete v [tomto vlákně StackOverflow](http://stackoverflow.com/questions/15467373/signalr-1-0-1-cross-domain-request-cors-with-chrome).
> - Ukázkový kód používá výchozí adresu URL "/signalr" pro připojení ke službě SignalR. Informace o tom, jak zadat jinou základní adresu URL, naleznete [v tématu ASP.NET SignalR Hubs API Guide - Server - Adresa URL /signalr](hubs-api-guide-server.md#signalrurl).

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a>Jak nakonfigurovat připojení

Před navázáním připojení můžete zadat parametry řetězce dotazu nebo zadat metodu přenosu.

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a>Jak zadat parametry řetězce dotazu

Pokud chcete odeslat data na server, když se klient připojí, můžete k objektu připojení přidat parametry řetězce dotazu. Následující příklady ukazují, jak nastavit parametr řetězce dotazu v kódu klienta.

**Nastavení hodnoty řetězce dotazu před voláním metody start (s vygenerovaným proxy serverem)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample12.js?highlight=1)]

**Nastavení hodnoty řetězce dotazu před voláním metody start (bez generovaného proxy serveru)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample13.js?highlight=2)]

Následující příklad ukazuje, jak číst parametr řetězce dotazu v kódu serveru.

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample14.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a>Jak určit způsob přenosu

V rámci procesu připojení klient SignalR obvykle vyjedná se serverem určit nejlepší přenos, který je podporován serverem i klientem. Pokud již víte, který přenos chcete použít, můžete tento proces vyjednávání obejít `start` zadáním metody přenosu při volání metody.

**Kód klienta, který určuje způsob přenosu (s vygenerovaným proxy serverem)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample15.js?highlight=1)]

**Kód klienta, který určuje způsob přenosu (bez generovaného proxy serveru)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample16.js?highlight=2)]

Jako alternativu můžete zadat více metod přenosu v pořadí, ve kterém chcete SignalR vyzkoušet:

**Kód klienta, který určuje záložní schéma vlastního přenosu (s generovaným proxy serverem)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample17.js?highlight=1)]

**Kód klienta, který určuje záložní schéma vlastního přenosu (bez generovaného proxy serveru)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample18.js?highlight=2)]

Pro určení způsobu přenosu můžete použít následující hodnoty:

- "webSockets"
- "foreverFrame"
- "serverSentEvents"
- "longPolling"

Následující příklady ukazují, jak zjistit, která způsob přenosu je používán připojení.

**Kód klienta, který zobrazuje způsob přenosu používaný připojením (s generovaným proxy serverem)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample19.js?highlight=2)]

**Kód klienta, který zobrazuje způsob přenosu používaný připojením (bez generovaného proxy serveru)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample20.js?highlight=3)]

Informace o tom, jak zkontrolovat metodu přenosu v kódu serveru, naleznete [v tématu ASP.NET SignalR Hubs API Guide - Server - Jak získat informace o klientovi z Context vlastnost](hubs-api-guide-server.md#contextproperty). Další informace o přenosu a záložních souborech naleznete [v tématu Úvod do SignalR - Transports a Fallbacks](../getting-started/introduction-to-signalr.md#transports).

<a id="getproxy"></a>

## <a name="how-to-get-a-proxy-for-a-hub-class"></a>Jak získat proxy pro třídu Hub

Každý objekt připojení, který vytvoříte zapouzdřit informace o připojení ke službě SignalR, která obsahuje jednu nebo více hub tříd. Chcete-li komunikovat s Hub třídy, použijte proxy objekt, který vytvoříte sami (pokud nepoužíváte generované proxy) nebo který je generován pro vás.

Na straně klienta je název proxy je camel-cased verze názvu třídy Hub. SignalR tuto změnu automaticky provede tak, aby kód JavaScript usměrňoval konvence JavaScriptu.

**Třída Hub na serveru**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample21.cs?highlight=1)]

**Získání odkazu na vygenerovaný proxy klienta pro centrum**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample22.js?highlight=1)]

**Vytvoření klientského proxy serveru pro třídu Hub (bez generovaného proxy serveru)**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample23.cs?highlight=1)]

Pokud vyzdobíte třídu Hub atributem, `HubName` použijte přesný název bez evidence.

**Třída Hub na serveru s atributem HubName**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample24.cs?highlight=1)]

**Získání odkazu na vygenerovaný proxy klienta pro centrum**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample25.js?highlight=1)]

**Vytvoření klientského proxy serveru pro třídu Hub (bez generovaného proxy serveru)**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample26.cs?highlight=1)]

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a>Jak definovat metody na straně klienta, který může server volat

Chcete-li definovat metodu, kterou může server volat z centra, přidejte obslužnou rutinu události do proxy centra pomocí `client` vlastnosti generovaného proxy serveru nebo tuto metodu `on` zavolejte, pokud nepoužíváte generovaný proxy server. Parametry mohou být složité objekty.

Před voláním metody k `start` navázání připojení přidejte obslužnou rutinu události. (Pokud chcete přidat obslužné `start` rutiny událostí po volání metody, naleznete v poznámce [Jak navázat připojení](#establishconnection) dříve v tomto dokumentu a použijte syntaxi zobrazenou pro definování metody bez použití generovaného proxy serveru.)

Porovnávání názvů metod nerozlišuje malá a velká písmena. Například `Clients.All.addContosoChatMessageToPage` na serveru bude `AddContosoChatMessageToPage` `addContosoChatMessageToPage`spuštěna `addcontosochatmessagetopage` , , nebo na straně klienta.

**Definovat metodu na straně klienta (s vygenerovaným proxy serverem)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample27.js?highlight=2)]

**Alternativní způsob definování metody na straně klienta (s vygenerovaným proxy serverem)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample28.js?highlight=1-2)]

**Definovat metodu na straně klienta (bez generovaného proxy serveru nebo při přidání po volání metody start)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample29.js?highlight=3)]

**Kód serveru, který volá metodu klienta**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample30.cs?highlight=5)]

Následující příklady zahrnují komplexní objekt jako parametr metody.

**Definovat metodu na klienta, který má složitý objekt (s generované proxy)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample31.js?highlight=2-3)]

**Definovat metodu na klienta, který má složitý objekt (bez generovaného proxy serveru)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample32.js?highlight=3-4)]

**Kód serveru, který definuje složitý objekt**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample33.cs?highlight=1)]

**Kód serveru, který volá metodu klienta pomocí komplexního objektu**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample34.cs?highlight=3)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a>Jak volat metody serveru z klienta

Chcete-li volat metodu serveru `server` z klienta, použijte `invoke` vlastnost generovaného proxy serveru nebo metodu na proxy centru, pokud nepoužíváte generovaný proxy server. Vrácená hodnota nebo parametry mohou být složité objekty.

Předajte v camel-case verzi názvu metody v centru. SignalR tuto změnu automaticky provede tak, aby kód JavaScript usměrňoval konvence JavaScriptu.

Následující příklady ukazují, jak volat metodu serveru, která nemá vrácenou hodnotu, a jak volat metodu serveru, která má vrácenou hodnotu.

**Metoda serveru bez atributu HubMethodName**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample35.cs?highlight=3)]

**Kód serveru, který definuje komplexní objekt předaný v parametru**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample36.cs)]

**Klientský kód, který vyvolá metodu serveru (s vygenerovaným proxy serverem)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample37.js?highlight=1)]

**Klientský kód, který vyvolá metodu serveru (bez generovaného proxy serveru)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample38.js?highlight=1)]

Pokud jste dekorované Hub `HubMethodName` metoda s atributem, použijte tento název beze změny případu.

**Metoda serveru** s atributem HubMethodName

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample39.cs?highlight=3)]

**Klientský kód, který vyvolá metodu serveru (s vygenerovaným proxy serverem)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample40.js?highlight=1)]

**Klientský kód, který vyvolá metodu serveru (bez generovaného proxy serveru)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample41.js?highlight=1)]

Předchozí příklady ukazují, jak volat metodu serveru, která nemá žádnou vrácenou hodnotu. Následující příklady ukazují, jak volat metodu serveru, která má vrácenou hodnotu.

**Kód serveru pro metodu, která má vrácenou hodnotu**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample42.cs?highlight=3)]

**Třída Stock použitá pro vrácenou** hodnotu

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample43.cs?highlight=1)]

**Klientský kód, který vyvolá metodu serveru (s vygenerovaným proxy serverem)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample44.js?highlight=2,4-5)]

**Klientský kód, který vyvolá metodu serveru (bez generovaného proxy serveru)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample45.js?highlight=2,4-5)]

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a>Jak zpracovat události životnosti připojení

SignalR poskytuje následující události životnosti připojení, které můžete zpracovat:

- `starting`: Vyvolána před odesláním dat přes připojení.
- `received`: Vyvolána při přijetí všech dat na připojení. Poskytuje přijatá data.
- `connectionSlow`: Aktivováno, když klient zjistí pomalé nebo často upadající připojení.
- `reconnecting`: Vyvolána při základní přenos začne znovu připojit.
- `reconnected`: Aktivováno, když je základní přenos znovu připojen.
- `stateChanged`: Aktivováno při změně stavu připojení. Poskytuje starý a nový stav (Připojení, Připojení, Opětovné připojení nebo Odpojeno).
- `disconnected`: Aktivováno po odpojení připojení.

Chcete-li například zobrazit varovné zprávy v případě problémů s připojením, které mohou způsobit znatelné zpoždění, zvládejte `connectionSlow` událost.

**Zpracování události connectionSlow (s vygenerovaným proxy serverem)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample46.js?highlight=1)]

**Zpracování události connectionSlow (bez generovaného proxy serveru)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample47.js?highlight=2)]

Další informace naleznete [v tématu Principy a zpracování událostí životnosti připojení v SignalR](handling-connection-lifetime-events.md).

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a>Jak zpracovat chyby

Klient JavaScript SignalR `error` poskytuje událost, pro kterou můžete přidat obslužnou rutinu. Metodu fail můžete také použít k přidání obslužné rutiny pro chyby, které vyplývají z vyvolání metody serveru.

Pokud explicitně nepovolíte podrobné chybové zprávy na serveru, objekt výjimky, který signalr vrátí po chybě, obsahuje minimální informace o chybě. Pokud se `newContosoChatMessage` například volání nezdaří, chybová zpráva`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`v objektu chyby obsahuje " Odesílání podrobných chybových zpráv klientům v produkčním prostředí se nedoporučuje z bezpečnostních důvodů, ale pokud chcete povolit podrobné chybové zprávy pro účely řešení potíží, použijte následující kód na serveru.

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample48.cs?highlight=2)]

Následující příklad ukazuje, jak přidat obslužnou rutinu pro událost chyby.

**Přidání obslužné rutiny chyby (s vygenerovaným proxy serverem)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample49.js?highlight=1)]

**Přidání obslužné rutiny chyby (bez generovaného proxy serveru)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample50.js?highlight=2)]

Následující příklad ukazuje, jak zpracovat chybu z vyvolání metody.

**Zpracování chyby z vyvolání metody (s vygenerovaným proxy serverem)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample51.js?highlight=2)]

**Zpracování chyby z vyvolání metody (bez generovaného proxy serveru)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample52.js?highlight=2)]

Pokud volání metody selže, `error` je vyvolána také událost, `error` takže váš `.fail` kód v obslužné rutině metody a v zpětném volání metody by se spustil.

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a>Jak povolit protokolování na straně klienta

Chcete-li povolit protokolování na `logging` straně klienta na připojení, `start` nastavte vlastnost objektu připojení před voláním metody k navázání připojení.

**Povolit protokolování (s vygenerovaným proxy serverem)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample53.js?highlight=1)]

**Povolit protokolování (bez generovaného proxy serveru)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample54.js?highlight=2)]

Chcete-li zobrazit protokoly, otevřete vývojářské nástroje prohlížeče a přejděte na kartu Konzola. Pro výukový program, který zobrazuje podrobné pokyny a snímky obrazovek, které ukazují, jak to udělat, naleznete [v tématu Vysílání serveru s ASP.NET Signalr - Povolit protokolování](../getting-started/tutorial-server-broadcast-with-signalr.md#enable-logging).
