---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-net-client
title: ASP.NET Průvodce rozhraním API center signalr - klient .NET (C#) | Dokumenty společnosti Microsoft
author: bradygaster
description: Tento dokument poskytuje úvod k použití rozhraní API hubs pro SignalR verze 2 v klientech .NET, jako je Windows Store (WinRT), WPF, Silverlight a nevýhody...
ms.author: bradyg
ms.date: 01/15/2019
ms.assetid: 6d02d9f7-94e5-4140-9f51-5a6040f274f6
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-net-client
msc.type: authoredcontent
ms.openlocfilehash: d3536f1c15cd7dad7cd660becf0577e5c131f707
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676333"
---
# <a name="aspnet-signalr-hubs-api-guide---net-client-c"></a>ASP.NET SignalR Hubs API Guide - klient .NET (C#)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Tento dokument poskytuje úvod k použití rozhraní API hubs pro SignalR verze 2 v klientech .NET, jako jsou Windows Store (WinRT), WPF, Silverlight a konzolové aplikace.
>
> Rozhraní API signalr hubs umožňuje provádět vzdálená volání procedur (RPC) ze serveru do připojených klientů a z klientů na server. V kódu serveru definujete metody, které mohou být volány klienty, a volání metod, které jsou spuštěny na straně klienta. V klientském kódu definujete metody, které lze volat ze serveru, a volání metod, které jsou spuštěny na serveru. SignalR se postará o všechny klient-to-server instalatérské pro vás.
>
> SignalR také nabízí rozhraní API nižší úrovně s názvem Trvalá připojení. Úvod do SignalR, Rozbočovače a trvalá připojení nebo pro kurz, který ukazuje, jak vytvořit kompletní aplikaci SignalR, naleznete v [tématu SignalR - Začínáme](../getting-started/index.md).
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

- [Nastavení klienta](#clientsetup)
- [Jak navázat spojení](#establishconnection)

    - [Připojení mezi doménami od klientů Silverlight](#slcrossdomain)
- [Jak nakonfigurovat připojení](#configureconnection)

    - [Jak nastavit maximální počet souběžných připojení v klientech WPF](#maxconnections)
    - [Jak zadat parametry řetězce dotazu](#querystring)
    - [Jak určit způsob přenosu](#transport)
    - [Jak zadat hlavičky HTTP](#httpheaders)
    - [Jak zadat klientské certifikáty](#clientcertificate)
- [Jak vytvořit server proxy hubu](#proxy)
- [Jak definovat metody na straně klienta, který může server volat](#callclient)

    - [Metody bez parametrů](#clientmethodswithoutparms)
    - [Metody s parametry, určení typů parametrů](#clientmethodswithparmtypes)
    - [Metody s parametry, určení dynamických objektů pro parametry](#clientmethodswithdynamparms)
    - [Odebrání obslužné rutiny](#removehandler)
- [Jak volat metody serveru z klienta](#callserver)
- [Jak zpracovat události životnosti připojení](#connectionlifetime)
- [Jak zpracovat chyby](#handleerrors)
- [Jak povolit protokolování na straně klienta](#logging)
- [Ukázky kódu aplikace WPF, Silverlight a konzoly pro klientské metody, které může server volat](#wpfsl)

Ukázkové klientské projekty .NET naleznete v následujících zdrojích:

- [gustavo-armenta / SignalR-Samples](https://github.com/gustavo-armenta/SignalR-Samples) on GitHub.com (WinRT, Silverlight, příklady konzolových aplikací).
- [DamianEdwards / SignalR-MoveShapeDemo / MoveShape.Desktop](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop) na GitHub.com (příklad WPF).
- [SignalR / Microsoft.AspNet.SignalR.Client.Samples](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples) na GitHub.com (příklad konzolové aplikace).

Dokumentaci k programování klientů jazyka JavaScript naleznete v následujících zdrojích informací:

- [Průvodce rozhraním API hubů SignalR – server](hubs-api-guide-server.md)
- [SignalR Hubs API Guide - Klient JavaScript](hubs-api-guide-javascript-client.md)

Odkazy na referenční témata rozhraní API jsou na verzi rozhraní .NET 4.5 rozhraní API. Pokud používáte rozhraní .NET 4, přečtěte si [verzi rozhraní API .NET 4](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx).

<a id="clientsetup"></a>

## <a name="client-setup"></a>Nastavení klienta

Nainstalujte balíček [Microsoft.AspNet.SignalR.Client](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client) NuGet (nikoli balíček [Microsoft.AspNet.SignalR).](http://nuget.org/packages/microsoft.aspnet.signalr) Tento balíček podporuje klienty WinRT, Silverlight, WPF, konzolové aplikace a Windows Phone pro rozhraní .NET 4 i .NET 4.5.

Pokud verze SignalR, které máte na straně klienta se liší od verze, kterou máte na serveru, SignalR je často schopen přizpůsobit se rozdílu. Například server se systémem SignalR verze 2 bude podporovat klienty s nainstalovanou verzí 1.1.x a také klienty, kteří mají nainstalovanou verzi 2. Pokud je rozdíl mezi verzí na serveru a verzí na straně klienta příliš velký nebo pokud je `InvalidOperationException` klient novější než server, signalr vyvolá výjimku, když se klient pokusí navázat připojení. Chybová zpráva`You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X`je " ".

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a>Jak navázat spojení

Před navázáním připojení je třeba `HubConnection` vytvořit objekt a vytvořit proxy server. Chcete-li navázat připojení, `Start` volání `HubConnection` metody na objektu.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample1.cs?highlight=1,5)]

> [!NOTE]
> Pro klienty JavaScriptu musíte před voláním `Start` metody k navázání připojení zaregistrovat alespoň jednu obslužnou rutinu události. To není nutné pro klienty .NET. Pro klienty JavaScriptu generovaný proxy kód automaticky vytvoří proxy servery pro všechna centra, která existují na serveru, a registrace obslužné rutiny je způsob, jakým označíte, které centra má váš klient v úmyslu použít. Ale pro klienta .NET vytvoříte servery proxy hub ručně, takže SignalR předpokládá, že budete používat libovolné centrum, pro které vytvoříte proxy server.

Ukázkový kód používá výchozí adresu URL "/signalr" pro připojení ke službě SignalR. Informace o tom, jak zadat jinou základní adresu URL, naleznete [v tématu ASP.NET SignalR Hubs API Guide - Server - Adresa URL /signalr](hubs-api-guide-server.md#signalrurl).

Metoda `Start` se provádí asynchronně. Chcete-li se ujistit, že následující řádky kódu se `await` nespustí až po navázání připojení, `.Wait()` použijte v ASP.NET 4.5 asynchronní metody nebo v synchronní metodě. Nepoužívejte `.Wait()` v klientovi WinRT.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample2.cs?highlight=1)]

[!code-css[Main](hubs-api-guide-net-client/samples/sample3.css?highlight=1)]

<a id="slcrossdomain"></a>

### <a name="cross-domain-connections-from-silverlight-clients"></a>Připojení mezi doménami od klientů Silverlight

Informace o povolení připojení mezi doménami z klientů Silverlight naleznete [v tématu Zpřístupnění služby přes hranice domény](https://msdn.microsoft.com/library/cc197955(v=vs.95).aspx).

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a>Jak nakonfigurovat připojení

Před navázáním připojení můžete určit některou z následujících možností:

- Limit souběžných připojení.
- Parametry řetězce dotazu.
- Způsob přenosu.
- Hlavičky HTTP.
- Klientské certifikáty.

<a id="maxconnections"></a>

### <a name="how-to-set-the-maximum-number-of-concurrent-connections-in-wpf-clients"></a>Jak nastavit maximální počet souběžných připojení v klientech WPF

V klientech WPF bude pravděpodobně muset zvýšit maximální počet souběžných připojení z výchozí hodnoty 2. Doporučená hodnota je 10.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample4.cs?highlight=5)]

Další informace naleznete v tématu [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx).

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a>Jak zadat parametry řetězce dotazu

Pokud chcete odeslat data na server, když se klient připojí, můžete k objektu připojení přidat parametry řetězce dotazu. Následující příklad ukazuje, jak nastavit parametr řetězce dotazu v kódu klienta.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample5.cs)]

Následující příklad ukazuje, jak číst parametr řetězce dotazu v kódu serveru.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample6.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a>Jak určit způsob přenosu

V rámci procesu připojení klient SignalR obvykle vyjedná se serverem určit nejlepší přenos, který je podporován serverem i klientem. Pokud již víte, který přenos chcete použít, můžete tento proces vyjednávání obejít. Chcete-li určit metodu přenosu, přejděte v objektu přenosu do metody Start. Následující příklad ukazuje, jak určit metodu přenosu v kódu klienta.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample7.cs?highlight=5)]

Obor názvů [Microsoft.AspNet.SignalR.Client.Transports](https://msdn.microsoft.com/library/jj918090(v=vs.111).aspx) obsahuje následující třídy, které můžete použít k určení přenosu.

- [LongPollingTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.longpollingtransport(v=vs.111).aspx)
- [ServerSentEventsTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.serversenteventstransport(v=vs.111).aspx)
- [WebSocketTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx) (K dispozici pouze v případě, že server i klient používají rozhraní .NET 4.5.)
- [AutoTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx) (Automaticky vybere nejlepší přenos, který je podporován klientem i serverem. Toto je výchozí přenos. Předání této `Start` metody má stejný účinek jako nepředávání v ničem.)

Přenos ForeverFrame není zahrnuta v tomto seznamu, protože je používán pouze prohlížeči.

Informace o tom, jak zkontrolovat metodu přenosu v kódu serveru, naleznete [v tématu ASP.NET SignalR Hubs API Guide - Server - Jak získat informace o klientovi z Context vlastnost](hubs-api-guide-server.md#contextproperty). Další informace o přenosu a záložních souborech naleznete [v tématu Úvod do SignalR - Transports a Fallbacks](../getting-started/introduction-to-signalr.md#transports).

<a id="httpheaders"></a>

### <a name="how-to-specify-http-headers"></a>Jak zadat hlavičky HTTP

Chcete-li nastavit záhlaví `Headers` protokolu HTTP, použijte vlastnost objektu připojení. Následující příklad ukazuje, jak přidat hlavičku HTTP.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample8.cs?highlight=2)]

<a id="clientcertificate"></a>

### <a name="how-to-specify-client-certificates"></a>Jak zadat klientské certifikáty

Chcete-li přidat klientské `AddClientCertificate` certifikáty, použijte metodu na objektu připojení.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample9.cs?highlight=2)]

<a id="proxy"></a>

## <a name="how-to-create-the-hub-proxy"></a>Jak vytvořit server proxy hubu

Chcete-li definovat metody na straně klienta, který může centrum volat ze serveru, a vyvolat metody v `CreateHubProxy` centru na serveru, vytvořte proxy server pro centrum voláním objektu připojení. Řetězec, do `CreateHubProxy` kterého se předáváte, je název třídy `HubName` Hub nebo název určený atributem, pokud byl použit na serveru. Porovnávání názvů nerozlišuje malá a velká písmena.

**Třída Hub na serveru**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample10.cs?highlight=1)]

**Vytvoření klientského proxy serveru pro třídu Hub**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample11.cs?highlight=3)]

Pokud vyzdobíte třídu Hub atributem, `HubName` použijte tento název.

**Třída Hub na serveru**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample12.cs)]

**Vytvoření klientského proxy serveru pro třídu Hub**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample13.cs?highlight=3)]

Pokud zavoláte `HubConnection.CreateHubProxy` vícekrát `hubName`se stejným , získáte `IHubProxy` stejný objekt uložený v mezipaměti.

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a>Jak definovat metody na straně klienta, který může server volat

Chcete-li definovat metodu, kterou může server `On` volat, použijte metodu proxy k registraci obslužné rutiny události.

Porovnávání názvů metod nerozlišuje malá a velká písmena. Například `Clients.All.UpdateStockPrice` na serveru bude `updateStockPrice` `updatestockprice`spuštěna `UpdateStockPrice` , , nebo na straně klienta.

Různé klientské platformy mají různé požadavky na způsob psaní kódu metody pro aktualizaci ui. Uvedené příklady jsou pro klienty WinRT (Windows Store .NET). Příklady aplikací WPF, Silverlight a konzoly jsou uvedeny v [samostatné části dále v tomto tématu](#wpfsl).

<a id="clientmethodswithoutparms"></a>

### <a name="methods-without-parameters"></a>Metody bez parametrů

Pokud metoda, kterou zpracováváte, nemá parametry, použijte neobecné `On` přetížení metody:

**Klientská metoda volání kódu serveru bez parametrů**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample14.cs?highlight=5)]

**Kód klienta WinRT pro metodu volanou ze serveru bez parametrů[(viz příklady WPF a Silverlight dále v tomto tématu)](#wpfsl)**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample15.cs)]

<a id="clientmethodswithparmtypes"></a>

### <a name="methods-with-parameters-specifying-the-parameter-types"></a>Metody s parametry, určení typů parametrů

Pokud metoda, kterou zpracováváte, má parametry, zadejte typy parametrů `On` jako obecné typy metody. Existují obecné přetížení `On` metody, která vám umožní zadat až 8 parametrů (4 na Windows Phone 7). V následujícím příkladu je do `UpdateStockPrice` metody odeslán jeden parametr.

**Serverkód volá metodu klienta s parametrem**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample16.cs?highlight=3)]

**Třída Stock použitá pro parametr**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample17.cs)]

**Kód klienta WinRT pro metodu volanou ze serveru s parametrem[(viz příklady WPF a Silverlight dále v tomto tématu)](#wpfsl)**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample18.cs?highlight=1,5)]

<a id="clientmethodswithdynamparms"></a>

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a>Metody s parametry, určení dynamických objektů pro parametry

Jako alternativu k určení parametrů jako `On` obecných typů metody můžete zadat parametry jako dynamické objekty:

**Serverkód volá metodu klienta s parametrem**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample19.cs?highlight=3)]

**Třída Stock použitá pro parametr**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample20.cs)]

**Kód klienta WinRT pro metodu volanou ze serveru s parametrem pomocí dynamického objektu pro parametr[(viz příklady WPF a Silverlight dále v tomto tématu)](#wpfsl)**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample21.cs?highlight=1,5)]

<a id="removehandler"></a>

### <a name="how-to-remove-a-handler"></a>Odebrání obslužné rutiny

Chcete-li odebrat `Dispose` obslužnou rutinu, zavolejte její metodu.

**Kód klienta pro metodu volanou ze serveru**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample22.cs?highlight=1)]

**Kód klienta pro odebrání obslužné rutiny**

[!code-css[Main](hubs-api-guide-net-client/samples/sample23.css?highlight=1)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a>Jak volat metody serveru z klienta

Chcete-li volat metodu na `Invoke` serveru, použijte metodu na proxy hubu.

Pokud metoda serveru nemá žádnou vrácenou hodnotu, `Invoke` použijte neobecné přetížení metody.

**Kód serveru pro metodu, která nemá žádnou vrácenou hodnotu**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample24.cs?highlight=3)]

**Kód klienta volající metodu, která nemá žádnou vrácenou hodnotu**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample25.cs?highlight=1)]

Pokud má metoda serveru vrácenou hodnotu, zadejte jako `Invoke` obecný typ metody návratový typ.

**Kód serveru pro metodu, která má vrácenou hodnotu a přebírá parametr komplexního typu**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample26.cs?highlight=1)]

**Třída Stock použitá pro parametr a vrácenou hodnotu**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample27.cs)]

**Klientský kód volající metodu, která má vrácenou hodnotu a přebírá parametr komplexního typu v ASP.NET asynchronní metodě 4.5**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample28.cs?highlight=1-2)]

**Klientský kód volající metodu, která má vrácenou hodnotu a přebírá parametr komplexního typu v synchronní metodě**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample29.cs?highlight=1-2)]

Metoda `Invoke` se spustí asynchronně a `Task` vrátí objekt. Pokud nezadáte `await` nebo `.Wait()`, další řádek kódu se spustí před metoda, kterou vyvolat dokončil provádění.

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a>Jak zpracovat události životnosti připojení

SignalR poskytuje následující události životnosti připojení, které můžete zpracovat:

- `Received`: Vyvolána při přijetí všech dat na připojení. Poskytuje přijatá data.
- `ConnectionSlow`: Aktivováno, když klient zjistí pomalé nebo často upadající připojení.
- `Reconnecting`: Vyvolána při základní přenos začne znovu připojit.
- `Reconnected`: Aktivováno, když je základní přenos znovu připojen.
- `StateChanged`: Aktivováno při změně stavu připojení. Poskytuje starý a nový stav. Informace o hodnotách stavu připojení naleznete v [tématu ConnectionState Enumeration](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx).
- `Closed`: Aktivováno po odpojení připojení.

Chcete-li například zobrazit varovné zprávy pro chyby, které nejsou závažné, ale způsobit občasné `ConnectionSlow` problémy s připojením, jako je například pomalost nebo časté přetažení připojení, zpracovat událost.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample30.cs)]

Další informace naleznete [v tématu Principy a zpracování událostí životnosti připojení v SignalR](handling-connection-lifetime-events.md).

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a>Jak zpracovat chyby

Pokud explicitně nepovolíte podrobné chybové zprávy na serveru, objekt výjimky, který signalr vrátí po chybě, obsahuje minimální informace o chybě. Pokud se `newContosoChatMessage` například volání nezdaří, chybová zpráva`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`v objektu chyby obsahuje " Odesílání podrobných chybových zpráv klientům v produkčním prostředí se nedoporučuje z bezpečnostních důvodů, ale pokud chcete povolit podrobné chybové zprávy pro účely řešení potíží, použijte následující kód na serveru.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample31.cs?highlight=2)]

<a id="handleerrors"></a>

Chcete-li zpracovat chyby, které signalr `Error` vyvolává, můžete přidat obslužnou rutinu pro událost na objekt připojení.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample32.cs)]

Chcete-li zpracovat chyby z vyvolání metody, zabalte kód do bloku try-catch.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample33.cs)]

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a>Jak povolit protokolování na straně klienta

Chcete-li povolit protokolování `TraceLevel` `TraceWriter` na straně klienta, nastavte vlastnosti a na objektu připojení.

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample34.cs?highlight=3-4)]

<a id="wpfsl"></a>

## <a name="wpf-silverlight-and-console-application-code-samples-for-client-methods-that-the-server-can-call"></a>Ukázky kódu aplikace WPF, Silverlight a konzoly pro klientské metody, které může server volat

Vzorky kódu zobrazené dříve pro definování klientských metod, které může server volat, platí pro klienty WinRT. Následující ukázky ukazují ekvivalentní kód pro wpf, Silverlight a konzolové aplikační klienty.

### <a name="methods-without-parameters"></a>Metody bez parametrů

**Kód klienta WPF pro metodu volanou ze serveru bez parametrů**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample35.cs?highlight=1)]

**Kód klienta Silverlight pro metodu volanou ze serveru bez parametrů**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample36.cs?highlight=1)]

**Klientský kód konzoly pro metodu volanou ze serveru bez parametrů**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample37.cs?highlight=1)]

### <a name="methods-with-parameters-specifying-the-parameter-types"></a>Metody s parametry, určení typů parametrů

**Kód klienta WPF pro metodu volanou ze serveru s parametrem**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample38.cs?highlight=1,4)]

**Kód klienta Silverlight pro metodu volanou ze serveru s parametrem**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample39.cs?highlight=1,5)]

**Kód klienta konzoly pro metodu volanou ze serveru s parametrem**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample40.cs?highlight=1-2)]

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a>Metody s parametry, určení dynamických objektů pro parametry

**Kód klienta WPF pro metodu volanou ze serveru s parametrem, pomocí dynamického objektu pro parametr**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample41.cs?highlight=1,4)]

**Kód klienta Silverlight pro metodu volanou ze serveru s parametrem pomocí dynamického objektu pro parametr**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample42.cs?highlight=1,5)]

**Klientský kód konzoly pro metodu volanou ze serveru s parametrem, pomocí dynamického objektu pro parametr**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample43.cs?highlight=1-2)]
