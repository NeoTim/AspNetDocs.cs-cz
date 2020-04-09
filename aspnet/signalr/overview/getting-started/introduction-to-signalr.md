---
uid: signalr/overview/getting-started/introduction-to-signalr
title: Úvod do SignalR | Dokumenty společnosti Microsoft
author: bradygaster
description: Tento článek popisuje, co signalr je a některé řešení, které byl navržen k vytvoření.
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 0fab5e35-8c1f-43d4-8635-b8aba8766a71
msc.legacyurl: /signalr/overview/getting-started/introduction-to-signalr
msc.type: authoredcontent
ms.openlocfilehash: 8dbc31a5c8d59fa55dc5b513c1a51d24d18a685f
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676347"
---
# <a name="introduction-to-signalr"></a>Úvod ke knihovně SignalR

podle [Patrick Fletcher](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Tento článek popisuje, co signalr je a některé řešení, které byl navržen k vytvoření. 
> 
> ## <a name="questions-and-comments"></a>Dotazy a připomínky
> 
> Prosím, zanechte zpětnou vazbu o tom, jak se vám líbil tento výukový program a co bychom mohli zlepšit v komentářích v dolní části stránky. Máte-li otázky, které nejsou přímo spojeny s tutoriálu, můžete je odeslat do [fóra ASP.NET SignalR](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) nebo [StackOverflow.com](https://stackoverflow.com/questions/tagged/signalr).

## <a name="what-is-signalr"></a>Co je SignalR?

ASP.NET SignalR je knihovna pro vývojáře ASP.NET, která zjednodušuje proces přidávání webových funkcí v reálném čase do aplikací. Funkce webu v reálném čase je možnost mít serverový kód nabízený obsah připojeným klientům okamžitě, jakmile bude k dispozici, spíše než mít server čekat na klienta požadovat nová data.

SignalR lze použít k přidání jakékoli webové funkce "v reálném čase" do aplikace ASP.NET. Zatímco chat je často používán jako příklad, můžete udělat mnohem víc. Pokaždé, když uživatel aktualizuje webovou stránku zobrazit nová data nebo stránka implementuje [dlouhé dotazování](http://en.wikipedia.org/wiki/Push_technology#Long_polling) načíst nová data, je kandidátem pro použití SignalR. Mezi příklady patří řídicí panely a monitorovací aplikace, aplikace pro spolupráci (například simultánní úpravy dokumentů), aktualizace průběhu úloh a formuláře v reálném čase.

SignalR také umožňuje zcela nové typy webových aplikací, které vyžadují vysokofrekvenční aktualizace ze serveru, například hraní her v reálném čase.

SignalR poskytuje jednoduché rozhraní API pro vytváření vzdálených volání procedur mezi servery a klienty , které volají funkce Jazyka JavaScript v klientských prohlížečích (a dalších klientských platformách) z kódu .NET na straně serveru. SignalR také obsahuje rozhraní API pro správu připojení (například události připojení a odpojení) a seskupování připojení.

![Vyvolání metod s SignalR](introduction-to-signalr/_static/image1.png)

Služba SignalR automaticky řeší správu připojení a dovoluje vám vysílat zprávy pro všechny připojené klienty najednou, jako v chatovací místnosti. Můžete také odesílat zprávy konkrétním klientům. Připojení mezi klientem a serverem je trvalé, na rozdíl od klasického připojení HTTP, které se při každé komunikaci obnovuje.

SignalR podporuje funkci "server push", ve kterém kód serveru můžete volat do klientského kódu v prohlížeči pomocí vzdálené procedury volání (RPC), spíše než model požadavku odpověď společné na webu dnes.

Aplikace SignalR můžete škálovat na tisíce klientů pomocí vestavěné a externí ch odstupňovaných poskytovatelů.

Mezi vestavěné poskytovatele patří:
* [Service Bus](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.ServiceBus3)
* [SQL Server](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.SqlServer)
* [Redis](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.Redis)

Mezi poskytovatele třetích stran patří:
* [NCache](https://www.alachisoft.com/ncache/asp-net-core-signalr.html).

SignalR je open source, přístupný přes [GitHub](https://github.com/signalr).

## <a name="signalr-and-websocket"></a>SignalR a WebSocket

SignalR používá nový přenos WebSocket, pokud je k dispozici a přejde zpět na starší přenosy v případě potřeby. I když byste mohli určitě napsat aplikaci pomocí WebSocket přímo, pomocí SignalR znamená, že mnoho dalších funkcí, které budete muset implementovat, je již provedeno za vás. A co je nejdůležitější, to znamená, že můžete kód aplikace využít WebSocket bez nutnosti starat o vytvoření samostatné cesty kódu pro starší klienty. SignalR také chrání vás před museli starat o aktualizace WebSocket, protože SignalR je aktualizován na podporu změn v základní přenos, poskytuje aplikaci konzistentní rozhraní napříč verzemi WebSocket.

<a id="transports"></a>

## <a name="transports-and-fallbacks"></a>Transporty a záložní náklady

SignalR je abstrakce přes některé přenosy, které jsou nutné k práci v reálném čase mezi klientem a serverem. Připojení SignalR se spustí jako HTTP a je pak povýšen na připojení WebSocket, pokud je k dispozici. WebSocket je ideální přenos pro SignalR, protože umožňuje nejefektivnější využití paměti serveru, má nejnižší latenci a má nejvíce základních funkcí (například plně duplexní komunikace mezi klientem a serverem), ale má také nejpřísnější požadavky: WebSocket vyžaduje, aby server používat Windows Server 2012 nebo Windows 8 a .NET Framework 4.5. Pokud tyto požadavky nejsou splněny, SignalR se pokusí použít jiné přenosy k jeho připojení.

### <a name="html-5-transports"></a>HTML 5 transportů

Tyto přenosy závisí na podpoře [html 5](http://en.wikipedia.org/wiki/HTML5). Pokud prohlížeč klienta nepodporuje standard HTML 5, budou použity starší přenosy.

- **WebSocket** (pokud server i prohlížeč naznačují, že mohou podporovat Websocket). WebSocket je jediný přenos, který vytváří skutečné trvalé obousměrné připojení mezi klientem a serverem. WebSocket má však také nejpřísnější požadavky; je plně podporován pouze v nejnovějších verzích aplikací Microsoft Internet Explorer, Google Chrome a Mozilla Firefox a má pouze částečnou implementaci v jiných prohlížečích, jako je Opera a Safari.
- **Události odeslané serverem**, známé také jako EventSource (pokud prohlížeč podporuje události odeslaných serverem, což jsou v podstatě všechny prohlížeče kromě aplikace Internet Explorer.)

### <a name="comet-transports"></a>Přeprava komet

Následující přenosy jsou založeny na modelu webové aplikace [Comet,](http://en.wikipedia.org/wiki/Comet_(programming)) ve kterém prohlížeč nebo jiný klient udržuje dlouhodobý požadavek HTTP, který může server použít k nabízení dat klientovi, aniž by o něj klient konkrétně požádal.

- **Forever Frame** (pouze pro aplikaci Internet Explorer). Forever Frame vytvoří skrytý IFrame, který provede požadavek na koncový bod na serveru, který není dokončen. Server pak neustále odesílá klientovi skript, který je okamžitě spuštěn, a poskytuje jednosměrné připojení v reálném čase ze serveru do klienta. Připojení z klienta na server používá samostatné připojení ze serveru ke připojení klienta a podobně jako standardní požadavek HTTP je pro každou část dat, která je třeba odeslat, vytvořeno nové připojení.
- **Ajax dlouhé hlasování**. Dlouhé dotazování nevytvoří trvalé připojení, ale místo toho dotazuje server s požadavkem, který zůstane otevřený, dokud server neodpoví, v tomto okamžiku se připojení zavře a okamžitě se vyžádá nové připojení. To může zavést některé latence při obnovení připojení.

Další informace o tom, jaké přenosy jsou podporovány v rámci které konfigurace, naleznete v [tématu podporované platformy](supported-platforms.md).

### <a name="transport-selection-process"></a>Proces výběru dopravy

Následující seznam uvádí kroky, které SignalR používá k rozhodnutí, který přenos použít.

1. Pokud je v prohlížeči internet explorer 8 nebo starší, používá se dlouhé dotazování.
2. Pokud je nakonfigurován JSONP `jsonp` (to znamená, že parametr je nastaven na `true` při spuštění připojení), dlouhé dotazování se používá.
3. Pokud je nastoano připojení mezi doménami (to znamená, že koncový bod SignalR není ve stejné doméně jako hostitelská stránka), bude websocket použit, pokud jsou splněna následující kritéria:

   - Klient podporuje CORS (Cross-Origin Resource Sharing). Podrobnosti o tom, kteří klienti podporují CORS, naleznete [v tématu CORS at caniuse.com](http://www.caniuse.com/CORS).
   - Klient podporuje websocket
   - Server podporuje websocket

     Pokud některé z těchto kritérií nejsou splněny, bude použit dlouhý dotazování. Další informace o připojení mezi doménami naleznete v [tématu Jak navázat připojení mezi doménami](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).
4. Pokud není program JSONP nakonfigurován a připojení není mezi doménami, bude použito websocket, pokud jej klient i server podporují.
5. Pokud klient nebo server nepodporují websocket, server odeslané události se používá, pokud je k dispozici.
6. Pokud události odeslané serverem nejsou k dispozici, dojde k pokusu o program Forever Frame.
7. Pokud forever frame selže, používá se dlouhé dotazování.

<a id="MonitoringTransports"></a>
### <a name="monitoring-transports"></a>Sledování přeprav

Můžete určit, jaký přenos aplikace používá povolením protokolování v rozbočovači a otevřením okna konzoly v prohlížeči.

Chcete-li povolit protokolování událostí v rozbočovači v prohlížeči, přidejte do klientské aplikace následující příkaz:

`$.connection.hub.logging = true;`

- V Aplikaci Internet Explorer otevřete vývojářské nástroje stisknutím klávesy F12 a klikněte na kartu Konzola.

    ![Konzola v aplikaci Microsoft Internet Explorer](introduction-to-signalr/_static/image2.png)
- V Chromu otevřete konzoli stisknutím ctrl+shift+j.

    ![Konzole v prohlížeči Google Chrome](introduction-to-signalr/_static/image3.png)

Když je konzole otevřená a protokolování je povolena, budete moci zjistit, který přenos používá SignalR.

![Konzola v aplikaci Internet Explorer zobrazující přenos websocketu](introduction-to-signalr/_static/image4.png)

### <a name="specifying-a-transport"></a>Určení přepravy

Vyjednávání přenosu trvá určité množství času a prostředky klient/server. Pokud jsou známy možnosti klienta, pak přenos lze zadat při spuštění připojení klienta. Následující fragment kódu ukazuje spuštění připojení pomocí přenosu Ajax Long Polling, jak by se použilo, pokud by bylo známo, že klient nepodporuje žádný jiný protokol:

`connection.start({ transport: 'longPolling' });`

Záložní objednávku můžete zadat, pokud chcete, aby klient vyzkoušel konkrétní přenosy v pořadí. Následující fragment kódu ukazuje pokus websocket a není-li to, jít přímo do dlouhé dotazování.

`connection.start({ transport: ['webSockets','longPolling'] });`

Konstanty řetězce pro určení transportů jsou definovány takto:

- `webSockets`
- `foreverFrame`
- `serverSentEvents`
- `longPolling`

## <a name="connections-and-hubs"></a>Připojení a rozbočovače

Rozhraní API signalr obsahuje dva modely pro komunikaci mezi klienty a servery: Trvalá připojení a Centra.

Připojení představuje jednoduchý koncový bod pro odesílání zpráv s jedním příjemcem, seskupených nebo všesměrových zpráv. Rozhraní PERSISTENT Connection API (reprezentované v kódu rozhraní .NET třídou PersistentConnection) poskytuje vývojáři přímý přístup ke komunikačnímu protokolu nižší úrovně, který signalr zveřejňuje. Pomocí komunikačního modelu připojení bude známé vývojářům, kteří používají rozhraní API založené na připojení, jako je například Windows Communication Foundation.

Rozbočovač je více kanál vyšší úrovně postavený na rozhraní API připojení, které umožňuje klientovi a serveru volat metody na sebe přímo. SignalR zpracovává dispečink přes hranice počítače, jako by magie, umožňuje klientům volat metody na serveru stejně snadno jako místní metody a naopak. Pomocí komunikačního modelu Rozbočovače budou vývojáři, kteří používají rozhraní API vzdáleného vyvolání, jako je například vzdálená komunikace .NET. Použití Hub také umožňuje předat silně zadaný parametry metody, povolení vazby modelu.

### <a name="architecture-diagram"></a>Diagram architektury

Následující diagram znázorňuje vztah mezi rozbočovači, trvalá připojení a základní technologie používané pro přenosy.

![Diagram architektury SignalR zobrazující api, přenosy a klienty](introduction-to-signalr/_static/image5.png)

### <a name="how-hubs-work"></a>Jak centra fungují

Když kód na straně serveru volá metodu na straně klienta, paket je odeslán přes aktivní přenos, který obsahuje název a parametry metody, která má být volána (při odeslání objektu jako parametr metody je serializován pomocí JSON). Klient pak odpovídá název metody metody definované v kódu na straně klienta. Pokud je shoda, klientská metoda bude provedena pomocí dat deserializovaných parametrů.

Volání metody lze sledovat pomocí nástrojů, jako [je Fiddler.](http://fiddler2.com/) Následující obrázek znázorňuje volání metody odeslané ze serveru SignalR klientovi webového prohlížeče v podokně Protokoly fiddleru. Volání metody je odesíláno `MoveShapeHub`z centra s názvem a `updateShape`volaná metoda je volána .

![Zobrazení šumerového protokolu zobrazujícího provoz SignalR](introduction-to-signalr/_static/image6.png)

V tomto příkladu je název `H` centra identifikován parametrem; název metody je identifikován `M` parametrem a data odesílaná do `A` metody jsou identifikována parametrem. Aplikace, která vygenerovala tuto zprávu, je vytvořena v kurzu [High-Frequency Realtime.](tutorial-high-frequency-realtime-with-signalr.md)

### <a name="choosing-a-communication-model"></a>Výběr komunikačního modelu

Většina aplikací by měla používat rozhraní API hubs. Rozhraní API připojení lze použít v následujících případech:

- Je třeba zadat formát skutečné odeslané zprávy.
- Vývojář upřednostňuje práci s modelem zasílání zpráv a odesílání před modelem vzdáleného vyvolání.
- Existující aplikace, která používá model zasílání zpráv je portován pro použití SignalR.
